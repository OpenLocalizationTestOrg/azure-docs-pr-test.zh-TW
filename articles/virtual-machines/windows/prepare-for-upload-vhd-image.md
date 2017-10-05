---
title: "準備要上傳至 Azure 的 Windows VHD | Microsoft Docs"
description: "如何在上傳至 Azure 之前準備 Windows VHD 或 VHDX"
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
ms.openlocfilehash: aa1cec2ef11da6aa8a8c4089be36994ab5f61682
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-to-upload-to-azure"></a><span data-ttu-id="cfdac-103">準備 Windows VHD 或 VHDX 以上傳至 Azure</span><span class="sxs-lookup"><span data-stu-id="cfdac-103">Prepare a Windows VHD or VHDX to upload to Azure</span></span>
<span data-ttu-id="cfdac-104">將 Windows 虛擬機器 (VM) 從內部部署上傳至 Microsoft Azure 之前，您必須先準備虛擬硬碟 (VHD 或 VHDX)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-104">Before you upload a Windows  virtual machines (VM) from on-premises to Microsoft Azure, you must prepare the virtual hard disk (VHD or VHDX).</span></span> <span data-ttu-id="cfdac-105">Azure 只支援採用 VHD 檔案格式且具有固定大小磁碟的第 1 代 VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-105">Azure supports only generation 1 VMs that are in the VHD file format and have a fixed sized disk.</span></span> <span data-ttu-id="cfdac-106">允許的 VHD 大小上限為 1023 GB。</span><span class="sxs-lookup"><span data-stu-id="cfdac-106">The maximum size allowed for the VHD is 1,023 GB.</span></span> <span data-ttu-id="cfdac-107">您可以將第 1 代 VM 從 VHDX 檔案系統轉換為 VHD，以及從動態擴充磁碟轉換為固定大小的磁碟。</span><span class="sxs-lookup"><span data-stu-id="cfdac-107">You can convert a generation 1 VM from the VHDX file system to VHD and from a dynamically expanding disk to fixed-sized.</span></span> <span data-ttu-id="cfdac-108">但您無法變更 VM 的世代。</span><span class="sxs-lookup"><span data-stu-id="cfdac-108">But you can't change a VM's generation.</span></span> <span data-ttu-id="cfdac-109">如需詳細資訊，請參閱[應該在 Hyper-V 中建立第 1 代還是第 2 代的 VM](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-109">For more information, see [Should I create a generation 1 or 2 VM in Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>

<span data-ttu-id="cfdac-110">如需 Azure VM 支援原則的詳細資訊，請參閱[適用於 Microsoft Azure 虛擬機器的 Microsoft Server Software 支援](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-110">For more information about the support policy for Azure VM, see [Microsoft server software support for Microsoft Azure VMs](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).</span></span>

> [!Note]
> <span data-ttu-id="cfdac-111">本文中的指示適用於 64 位元版本的 Windows Server 2008 R2 或更新版本的 Windows Server 作業系統。</span><span class="sxs-lookup"><span data-stu-id="cfdac-111">The instructions in this article apply to the 64-bit version of Windows Server 2008 R2 and later Windows server operating system.</span></span> <span data-ttu-id="cfdac-112">如需 Azure 中執行 32 位元版本的作業系統相關資訊，請參閱[在 Azure 虛擬機器中對 32 位元作業系統的支援](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-112">For information about running 32-bit version of operating system in Azure, see [Support for 32-bit operating systems in Azure virtual machines](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).</span></span>

## <a name="convert-the-virtual-disk-to-vhd-and-fixed-size-disk"></a><span data-ttu-id="cfdac-113">將虛擬磁碟轉換成 VHD 及固定大小的磁碟</span><span class="sxs-lookup"><span data-stu-id="cfdac-113">Convert the virtual disk to VHD and fixed size disk</span></span> 
<span data-ttu-id="cfdac-114">如果您需要將虛擬磁碟轉換為 Azure 所需的格式，請使用本節中的其中一種方法。</span><span class="sxs-lookup"><span data-stu-id="cfdac-114">If you need to convert your virtual disk to the required format for Azure, use one of the methods in this section.</span></span> <span data-ttu-id="cfdac-115">在執行虛擬磁碟轉換程序之前備份 VM ，並確定 Windows VHD 在本機伺服器上正常運作。</span><span class="sxs-lookup"><span data-stu-id="cfdac-115">Back up the VM before you run the virtual disk conversion process and make sure that the Windows VHD works correctly on the local server.</span></span> <span data-ttu-id="cfdac-116">先解決 VM 本身的任何錯誤，然後嘗試轉換或上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="cfdac-116">Resolve any errors within the VM itself before you try to convert or upload it to Azure.</span></span>

<span data-ttu-id="cfdac-117">在轉換磁碟之後，建立會使用轉換磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-117">After you convert the disk, create a VM that uses the converted disk.</span></span> <span data-ttu-id="cfdac-118">啟動並登入 VM 以完成準備上傳 VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-118">Start and sign in to the VM to finish preparing the VM for upload.</span></span>

### <a name="convert-disk-using-hyper-v-manager"></a><span data-ttu-id="cfdac-119">使用 HYPER-V 管理員轉換磁碟</span><span class="sxs-lookup"><span data-stu-id="cfdac-119">Convert disk using Hyper-V Manager</span></span>
1. <span data-ttu-id="cfdac-120">開啟 Hyper-V 管理員，然後在左側選取您的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="cfdac-120">Open Hyper-V Manager and select your local computer on the left.</span></span> <span data-ttu-id="cfdac-121">在電腦清單上方的功能表中，按一下 [動作] >  [編輯磁碟]。</span><span class="sxs-lookup"><span data-stu-id="cfdac-121">In the menu above the computer list, click **Action** > **Edit Disk**.</span></span>
2. <span data-ttu-id="cfdac-122">在 [尋找虛擬硬碟] 畫面上，尋找並選取您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="cfdac-122">On the **Locate Virtual Hard Disk** screen, locate and select your virtual disk.</span></span>
3. <span data-ttu-id="cfdac-123">在 [選擇動作] 畫面上，接著選取 [轉換] 和 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cfdac-123">On the **Choose Action** screen, and then select **Convert** and **Next**.</span></span>
4. <span data-ttu-id="cfdac-124">如果您需要從 VHDX 進行轉換，選取 [VHD]，然後按 [下一步]</span><span class="sxs-lookup"><span data-stu-id="cfdac-124">If you need to convert from VHDX, select **VHD** and then click **Next**</span></span>
5. <span data-ttu-id="cfdac-125">如果您需要從動態擴充磁碟進行轉換，選取 [固定大小]，然後按 [下一步]</span><span class="sxs-lookup"><span data-stu-id="cfdac-125">If you need to convert from a dynamically expanding disk, select **Fixed size** and then click **Next**</span></span>
6. <span data-ttu-id="cfdac-126">尋找並選取用以儲存新 VHD 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="cfdac-126">Locate and select a path to save the new VHD file to.</span></span>
7. <span data-ttu-id="cfdac-127">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="cfdac-127">Click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="cfdac-128">本文中的命令必須以提高權限的 PowerShell 工作階段來執行。</span><span class="sxs-lookup"><span data-stu-id="cfdac-128">The commands in this article must be run on an elevated PowerShell session.</span></span>

### <a name="convert-disk-by-using-powershell"></a><span data-ttu-id="cfdac-129">使用 PowerShell 轉換磁碟</span><span class="sxs-lookup"><span data-stu-id="cfdac-129">Convert disk by using PowerShell</span></span>
<span data-ttu-id="cfdac-130">您可以在 Windows PowerShell 中使用 [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) 命令來轉換虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="cfdac-130">You can convert a virtual disk by using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) command in Windows PowerShell.</span></span> <span data-ttu-id="cfdac-131">當您啟動 PowerShell 時，選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="cfdac-131">Select **Run as administrator** when you start PowerShell.</span></span> 

<span data-ttu-id="cfdac-132">下列範例命令會從 VHDX 轉換至 VHD，以及從動態擴充磁碟轉換至固定大小的磁碟：</span><span class="sxs-lookup"><span data-stu-id="cfdac-132">The following example command converts from VHDX to VHD, and from a dynamically expanding disk to fixed-size:</span></span>

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
<span data-ttu-id="cfdac-133">在這個命令中，使用您想要轉換的虛擬硬碟路徑取代 "-Path" 的值，並使用已轉換磁碟的新路徑和名稱取代 "-DestinationPath" 的值。</span><span class="sxs-lookup"><span data-stu-id="cfdac-133">In this command, replace the value for "-Path" with the path to the virtual hard disk that you want to convert and the value for "-DestinationPath" with the new path and name of the converted disk.</span></span>

### <a name="convert-from-vmware-vmdk-disk-format"></a><span data-ttu-id="cfdac-134">從 VMware VMDK 磁碟格式進行轉換</span><span class="sxs-lookup"><span data-stu-id="cfdac-134">Convert from VMware VMDK disk format</span></span>
<span data-ttu-id="cfdac-135">如果您的 Windows VM 映像是 [VMDK 檔案格式](https://en.wikipedia.org/wiki/VMDK)，使用 [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497) \(英文\) 將它轉換為 VHD。</span><span class="sxs-lookup"><span data-stu-id="cfdac-135">If you have a Windows VM image in the [VMDK file format](https://en.wikipedia.org/wiki/VMDK), convert it to a VHD by using the [Microsoft VM Converter](https://www.microsoft.com/download/details.aspx?id=42497).</span></span> <span data-ttu-id="cfdac-136">如需詳細資訊，請參閱部落格文章：[如何將 VMware VMDK 轉換為 Hyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-136">For more information, see the blog article [How to Convert a VMware VMDK to Hyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).</span></span>

## <a name="set-windows-configurations-for-azure"></a><span data-ttu-id="cfdac-137">設定適用於 Azure 的 Windows 設定</span><span class="sxs-lookup"><span data-stu-id="cfdac-137">Set Windows configurations for Azure</span></span>

<span data-ttu-id="cfdac-138">在您計劃上傳至 Azure 的 VM 上，於下列步驟中，從[提升權限的命令提示字元視窗](https://technet.microsoft.com/library/cc947813.aspx)執行所有命令：</span><span class="sxs-lookup"><span data-stu-id="cfdac-138">On the VM that you plan to upload to Azure, run all commands in the following steps from an [elevated Command Prompt window](https://technet.microsoft.com/library/cc947813.aspx):</span></span>

1. <span data-ttu-id="cfdac-139">在路由表上移除任何靜態持續路由：</span><span class="sxs-lookup"><span data-stu-id="cfdac-139">Remove any static persistent route on the routing table:</span></span>
   
   * <span data-ttu-id="cfdac-140">若要檢視路由表，在命令提示字元視窗上執行 `route print`。</span><span class="sxs-lookup"><span data-stu-id="cfdac-140">To view the route table, run `route print` at the command prompt.</span></span>
   * <span data-ttu-id="cfdac-141">檢查 [持續路由]  區段。</span><span class="sxs-lookup"><span data-stu-id="cfdac-141">Check the **Persistence Routes** sections.</span></span> <span data-ttu-id="cfdac-142">如果有持續的路由，請使用 [route delete](https://technet.microsoft.com/library/cc739598.apx) 加以移除。</span><span class="sxs-lookup"><span data-stu-id="cfdac-142">If there is a persistent route, use [route delete](https://technet.microsoft.com/library/cc739598.apx) to remove it.</span></span>
2. <span data-ttu-id="cfdac-143">移除 WinHTTP Proxy：</span><span class="sxs-lookup"><span data-stu-id="cfdac-143">Remove the WinHTTP proxy:</span></span>
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. <span data-ttu-id="cfdac-144">將磁碟 SAN 原則設為 [Onlineall](https://technet.microsoft.com/library/gg252636.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-144">Set the disk SAN policy to [Onlineall](https://technet.microsoft.com/library/gg252636.aspx).</span></span> 
   
    ```PowerShell
    diskpart 
    ```
    <span data-ttu-id="cfdac-145">在開啟的命令提示字元視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="cfdac-145">In the open Command Prompt window, type the following commands:</span></span>

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. <span data-ttu-id="cfdac-146">設定適用於 Windows 的國際標準時間 (UTC)，並將 Windows 時間 (w32time) 服務的啟動類型設為 [自動]：</span><span class="sxs-lookup"><span data-stu-id="cfdac-146">Set Coordinated Universal Time (UTC) time for Windows and the startup type of the Windows Time (w32time) service to **Automatically**:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. <span data-ttu-id="cfdac-147">將電源設定檔設為 [高效能]：</span><span class="sxs-lookup"><span data-stu-id="cfdac-147">Set the power profile to the **High Performance**:</span></span>

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-the-windows-services"></a><span data-ttu-id="cfdac-148">檢查 Windows 服務</span><span class="sxs-lookup"><span data-stu-id="cfdac-148">Check the Windows services</span></span>
<span data-ttu-id="cfdac-149">確定以下的每個 Windows 服務都已設為 **Windows 預設值**。</span><span class="sxs-lookup"><span data-stu-id="cfdac-149">Make sure that each of the following Windows services is set to the **Windows default values**.</span></span> <span data-ttu-id="cfdac-150">這些是必須設定來確定 VM 具有連線能力的服務最小數目。</span><span class="sxs-lookup"><span data-stu-id="cfdac-150">These are the minimum numbers of services that must be set up to make sure that the VM has connectivity.</span></span> <span data-ttu-id="cfdac-151">若要重設啟動設定，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cfdac-151">To reset the startup settings, run the following commands:</span></span>
   
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

## <a name="update-remote-desktop-registry-settings"></a><span data-ttu-id="cfdac-152">更新遠端桌面登錄設定</span><span class="sxs-lookup"><span data-stu-id="cfdac-152">Update Remote Desktop registry settings</span></span>
<span data-ttu-id="cfdac-153">確定已針對遠端桌面連線正確設定下列設定：</span><span class="sxs-lookup"><span data-stu-id="cfdac-153">Make sure that the following settings are configured correctly for remote desktop connection:</span></span>

>[!Note] 
><span data-ttu-id="cfdac-154">當您在這些步驟中執行 **Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services -name &lt;物件名稱&gt; &lt;值&gt;** 時，可能會收到一則錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cfdac-154">You may receive an error message when you run the **Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services -name &lt;object name&gt; &lt;value&gt;** in these steps.</span></span> <span data-ttu-id="cfdac-155">您可以放心地忽略該錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cfdac-155">The error message can be safely ignored.</span></span> <span data-ttu-id="cfdac-156">它只是表示網域不是透過群組原則物件來推送該設定。</span><span class="sxs-lookup"><span data-stu-id="cfdac-156">It means only that the domain is not pushing that configuration through a Group Policy object.</span></span>
>
>

1. <span data-ttu-id="cfdac-157">遠端桌面通訊協定 (RDP) 已啟用：</span><span class="sxs-lookup"><span data-stu-id="cfdac-157">Remote Desktop Protocol (RDP) is enabled:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. <span data-ttu-id="cfdac-158">RDP 連接埠已正確設定 (預設連接埠 3389)：</span><span class="sxs-lookup"><span data-stu-id="cfdac-158">The RDP port is set up correctly (Default port 3389):</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    <span data-ttu-id="cfdac-159">當您部署 VM 時，會針對連接埠 3389 建立預設規則。</span><span class="sxs-lookup"><span data-stu-id="cfdac-159">When you deploy a VM, the default rules are created against port 3389.</span></span> <span data-ttu-id="cfdac-160">如果您想要變更連接埠號碼，請在 Azure 中部署 VM 之後進行。</span><span class="sxs-lookup"><span data-stu-id="cfdac-160">If you want to change the port number,  do that after the VM is deployed in Azure.</span></span>

3. <span data-ttu-id="cfdac-161">接聽程式正在每個網路介面中進行接聽：</span><span class="sxs-lookup"><span data-stu-id="cfdac-161">The listener is listening in every network interface:</span></span>
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. <span data-ttu-id="cfdac-162">設定 RDP 連線的網路層級驗證模式：</span><span class="sxs-lookup"><span data-stu-id="cfdac-162">Configure the Network Level Authentication mode for the RDP connections:</span></span>
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. <span data-ttu-id="cfdac-163">設定 Keep-Alive 值：</span><span class="sxs-lookup"><span data-stu-id="cfdac-163">Set the keep-alive value：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. <span data-ttu-id="cfdac-164">重新連線：</span><span class="sxs-lookup"><span data-stu-id="cfdac-164">Reconnect：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. <span data-ttu-id="cfdac-165">並行連線數目的限制：</span><span class="sxs-lookup"><span data-stu-id="cfdac-165">Limit the number of concurrent connections：</span></span>
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. <span data-ttu-id="cfdac-166">如果有任何自我簽署憑證繫結至 RDP 接聽程式，請移除它們：</span><span class="sxs-lookup"><span data-stu-id="cfdac-166">If there are any self-signed certificates tied to the RDP listener, remove them:</span></span>
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    <span data-ttu-id="cfdac-167">這是為了確定您在部署 VM 時，一開始就能連線。</span><span class="sxs-lookup"><span data-stu-id="cfdac-167">This is to make sure that you can connect at the beginning when you deploy the VM.</span></span> <span data-ttu-id="cfdac-168">您也可以視需要，在 Azure 中部署 VM 之後的後續階段中檢閱這部分。</span><span class="sxs-lookup"><span data-stu-id="cfdac-168">You can also review this on a later stage after the VM is deployed in Azure if needed.</span></span>

9. <span data-ttu-id="cfdac-169">如果 VM 將為網域的一部分，請檢查下列所有設定，以確定不會還原先前設定。</span><span class="sxs-lookup"><span data-stu-id="cfdac-169">If the VM will be part of a Domain, check all the following settings to make sure that the former settings are not reverted.</span></span> <span data-ttu-id="cfdac-170">以下為必須檢查的原則：</span><span class="sxs-lookup"><span data-stu-id="cfdac-170">The policies that must be checked are the following:</span></span>
    
    - <span data-ttu-id="cfdac-171">RDP 已啟用：</span><span class="sxs-lookup"><span data-stu-id="cfdac-171">RDP is enabled:</span></span>

         <span data-ttu-id="cfdac-172">電腦設定\原則\Windows 設定\系統管理範本\元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="cfdac-172">Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span>
         
         <span data-ttu-id="cfdac-173">**允許使用者使用遠端桌面服務從遠端連線**</span><span class="sxs-lookup"><span data-stu-id="cfdac-173">**Allow users to connect remotely by using Remote Desktop**</span></span>

    - <span data-ttu-id="cfdac-174">NLA 群組原則：</span><span class="sxs-lookup"><span data-stu-id="cfdac-174">NLA group policy:</span></span>

        <span data-ttu-id="cfdac-175">設定\系統管理範本\元件\遠端桌面服務\遠端桌面工作階段主機\安全性：</span><span class="sxs-lookup"><span data-stu-id="cfdac-175">Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security:</span></span> 
        
        <span data-ttu-id="cfdac-176">**透過使用網路層級驗證以要求對遠端連線進行使用者驗證**</span><span class="sxs-lookup"><span data-stu-id="cfdac-176">**Require user Authentication for remote connections by using Network Level Authentication**</span></span>
    
    - <span data-ttu-id="cfdac-177">Keep Alive 設定：</span><span class="sxs-lookup"><span data-stu-id="cfdac-177">Keep Alive settings:</span></span>

        <span data-ttu-id="cfdac-178">電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="cfdac-178">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="cfdac-179">**設定 Keep-Alive 連線間隔**</span><span class="sxs-lookup"><span data-stu-id="cfdac-179">**Configure keep-alive connection interval**</span></span>

    - <span data-ttu-id="cfdac-180">重新連線設定：</span><span class="sxs-lookup"><span data-stu-id="cfdac-180">Reconnect settings:</span></span>

        <span data-ttu-id="cfdac-181">電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="cfdac-181">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="cfdac-182">**自動重新連線**</span><span class="sxs-lookup"><span data-stu-id="cfdac-182">**Automatic reconnection**</span></span>

    - <span data-ttu-id="cfdac-183">限制連線數目的設定：</span><span class="sxs-lookup"><span data-stu-id="cfdac-183">Limit the number of connections settings:</span></span>

        <span data-ttu-id="cfdac-184">電腦設定\原則\Windows 設定\系統管理範本\Windows 元件\遠端桌面服務\遠端桌面工作階段主機\連線：</span><span class="sxs-lookup"><span data-stu-id="cfdac-184">Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections:</span></span> 
        
        <span data-ttu-id="cfdac-185">**限制連線數目**</span><span class="sxs-lookup"><span data-stu-id="cfdac-185">**Limit number of connections**</span></span>

## <a name="configure-windows-firewall-rules"></a><span data-ttu-id="cfdac-186">設定 Windows 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="cfdac-186">Configure Windows Firewall rules</span></span>
1. <span data-ttu-id="cfdac-187">在這三個設定檔 (網域、標準和公用) 上開啟 Windows 防火牆：</span><span class="sxs-lookup"><span data-stu-id="cfdac-187">Turn on Windows Firewall on the three profiles (Domain, Standard, and Public):</span></span>

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. <span data-ttu-id="cfdac-188">在 PowerShell 中執行下列命令，以允許 WinRM 透過這三種防火牆設定檔 (網域、私人和公用)，並啟用 PowerShell 遠端服務：</span><span class="sxs-lookup"><span data-stu-id="cfdac-188">Run the following command in PowerShell to allow WinRM through the three firewall profiles (Domain, Private, and Public) and enable the PowerShell Remote service:</span></span>
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. <span data-ttu-id="cfdac-189">啟用下列防火牆規則以允許 RDP 流量</span><span class="sxs-lookup"><span data-stu-id="cfdac-189">Enable the following firewall rules to allow the RDP traffic</span></span> 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. <span data-ttu-id="cfdac-190">啟用檔案及印表機共用規則，讓 VM 可以在虛擬網路內回應 ping 命令：</span><span class="sxs-lookup"><span data-stu-id="cfdac-190">Enable the File and Printer Sharing rule so that the VM can respond to a ping command inside the Virtual Network:</span></span>

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. <span data-ttu-id="cfdac-191">如果 VM 將為網域的一部分，請檢查下列設定，以確定不會還原先前設定。</span><span class="sxs-lookup"><span data-stu-id="cfdac-191">If the VM  will be part of a Domain, check the following settings to make sure that the former settings are not reverted.</span></span> <span data-ttu-id="cfdac-192">以下為必須檢查的 AD 原則：</span><span class="sxs-lookup"><span data-stu-id="cfdac-192">The AD policies that must be checked are the following:</span></span>

    - <span data-ttu-id="cfdac-193">啟用 Windows 防火牆設定檔</span><span class="sxs-lookup"><span data-stu-id="cfdac-193">Enable the Windows Firewall profiles</span></span>

        <span data-ttu-id="cfdac-194">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **保護所有網路連線**</span><span class="sxs-lookup"><span data-stu-id="cfdac-194">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Protect all network connections**</span></span>

       <span data-ttu-id="cfdac-195">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **保護所有網路連線**</span><span class="sxs-lookup"><span data-stu-id="cfdac-195">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Protect all network connections**</span></span>

    - <span data-ttu-id="cfdac-196">啟用 RDP</span><span class="sxs-lookup"><span data-stu-id="cfdac-196">Enable RDP</span></span> 

        <span data-ttu-id="cfdac-197">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **允許輸入的遠端桌面例外**</span><span class="sxs-lookup"><span data-stu-id="cfdac-197">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

        <span data-ttu-id="cfdac-198">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **允許輸入的遠端桌面例外**</span><span class="sxs-lookup"><span data-stu-id="cfdac-198">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow inbound Remote Desktop exceptions**</span></span>

    - <span data-ttu-id="cfdac-199">啟用 ICMP-V4</span><span class="sxs-lookup"><span data-stu-id="cfdac-199">Enable ICMP-V4</span></span>

        <span data-ttu-id="cfdac-200">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\網域設定檔\Windows 防火牆: **允許 ICMP 例外**</span><span class="sxs-lookup"><span data-stu-id="cfdac-200">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

        <span data-ttu-id="cfdac-201">電腦設定\原則\Windows 設定\系統管理範本\網路\網路連線\Windows 防火牆\標準設定檔\Windows 防火牆: **允許 ICMP 例外**</span><span class="sxs-lookup"><span data-stu-id="cfdac-201">Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Allow ICMP exceptions**</span></span>

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a><span data-ttu-id="cfdac-202">確認 VM 處於狀況良好、安全且可使用 RDP 存取</span><span class="sxs-lookup"><span data-stu-id="cfdac-202">Verify VM is healthy, secure, and accessible with RDP</span></span> 
1. <span data-ttu-id="cfdac-203">若要確定磁碟是狀況良好且一致的，在下一個 VM 重新啟動時，執行檢查磁碟作業：</span><span class="sxs-lookup"><span data-stu-id="cfdac-203">To make sure the disk is healthy and consistent, run a check disk operation at the next VM restart:</span></span>

    ```PowerShell
    Chkdsk /f
    ```
    <span data-ttu-id="cfdac-204">請確定此報告會顯示全新且狀況良好的磁碟。</span><span class="sxs-lookup"><span data-stu-id="cfdac-204">Make sure that the report shows a clean and healthy disk.</span></span>

2. <span data-ttu-id="cfdac-205">設定開機組態資料 (BCD) 設定。</span><span class="sxs-lookup"><span data-stu-id="cfdac-205">Set the Boot Configuration Data (BCD) settings.</span></span> 

    > [!Note]
    > <span data-ttu-id="cfdac-206">請確定您是在提升權限的 CMD 視窗上執行這些命令，而**不是**在 PowerShell 上：</span><span class="sxs-lookup"><span data-stu-id="cfdac-206">Make sure you run these commands on an elevated CMD window and **NOT** on PowerShell:</span></span>
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. <span data-ttu-id="cfdac-207">確認 Windows Management Instrumentation 存放庫是一致的。</span><span class="sxs-lookup"><span data-stu-id="cfdac-207">Verify that the Windows Management Instrumentations repository is consistent.</span></span> <span data-ttu-id="cfdac-208">若要執行此動作，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cfdac-208">To perform this, run the following command:</span></span>

    ```PowerShell
    winmgmt /verifyrepository
    ```
    <span data-ttu-id="cfdac-209">如果存放庫損毀，請參閱 [WMI︰存放庫損毀，還是沒有損毀](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-209">If the repository is corrupted, see [WMI: Repository Corruption, or Not](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).</span></span>

4. <span data-ttu-id="cfdac-210">確定沒有任何其他應用程式使用連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="cfdac-210">Make sure that any other application is not using the port 3389.</span></span> <span data-ttu-id="cfdac-211">在 Azure 中，此連接埠是由 RDP 服務所使用。</span><span class="sxs-lookup"><span data-stu-id="cfdac-211">This port is used for the RDP service in Azure.</span></span> <span data-ttu-id="cfdac-212">您可以執行 **netstat anob** 來查看 VM 上使用了哪些連接埠：</span><span class="sxs-lookup"><span data-stu-id="cfdac-212">You can run **netstat -anob** to see which ports are in used on the VM:</span></span>

    ```PowerShell
    netstat -anob
    ```

5. <span data-ttu-id="cfdac-213">如果您想要上傳的 Windows VHD 是一個網域控制站，則請遵循這些步驟：</span><span class="sxs-lookup"><span data-stu-id="cfdac-213">If the Windows VHD that you want to upload is a domain controller, then follow these steps:</span></span>

    <span data-ttu-id="cfdac-214">A.</span><span class="sxs-lookup"><span data-stu-id="cfdac-214">A.</span></span> <span data-ttu-id="cfdac-215">遵循[這些額外的步驟](https://support.microsoft.com/kb/2904015)來準備磁碟。</span><span class="sxs-lookup"><span data-stu-id="cfdac-215">Follow [these extra steps](https://support.microsoft.com/kb/2904015) to prepare the disk.</span></span>

    <span data-ttu-id="cfdac-216">B.</span><span class="sxs-lookup"><span data-stu-id="cfdac-216">B.</span></span> <span data-ttu-id="cfdac-217">確定您知道 DSRM 密碼，以防您必須在某個時間點於 DSRM 中啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-217">Make sure that you know the DSRM password in case you have to start the VM in DSRM at some point.</span></span> <span data-ttu-id="cfdac-218">您可能想要參考此連結來設定 [DSRM 密碼](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-218">You may want to refer to this link to set the [DSRM password](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).</span></span>

6. <span data-ttu-id="cfdac-219">確定您知道內建的系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="cfdac-219">Make sure that the Built-in Administrator account and password are known to you.</span></span> <span data-ttu-id="cfdac-220">您可能想要重設目前的本機系統管理員密碼，並確定您可以使用此帳戶，透過 RDP 連線登入 Windows。</span><span class="sxs-lookup"><span data-stu-id="cfdac-220">You may want to reset the current local administrator password and make sure that you can use this account to sign in to Windows through the RDP connection.</span></span> <span data-ttu-id="cfdac-221">此存取權限會受到「允許透過遠端桌面服務登入」群組原則物件所控制。</span><span class="sxs-lookup"><span data-stu-id="cfdac-221">This access permission is controlled by the "Allow log on through Remote Desktop Services" Group Policy object.</span></span> <span data-ttu-id="cfdac-222">您可以於下列位置的本機群組原則編輯器中檢視此物件：</span><span class="sxs-lookup"><span data-stu-id="cfdac-222">You can view this object in the Local Group Policy Editor under:</span></span>

    <span data-ttu-id="cfdac-223">電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派</span><span class="sxs-lookup"><span data-stu-id="cfdac-223">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment</span></span>

7. <span data-ttu-id="cfdac-224">請檢查下列 AD 原則，確定您並未封鎖透過 RDP 或來自網路的 RDP 存取：</span><span class="sxs-lookup"><span data-stu-id="cfdac-224">Check the following AD polices to make sure that you are not blocking your RDP access through RDP nor from the network:</span></span>

    - <span data-ttu-id="cfdac-225">電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派\拒絕從網路存取此電腦</span><span class="sxs-lookup"><span data-stu-id="cfdac-225">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny access to this computer from the network</span></span>

    - <span data-ttu-id="cfdac-226">電腦設定\Windows 設定\安全性設定\本機原則\使用者權限指派\拒絕從遠端桌面服務登入</span><span class="sxs-lookup"><span data-stu-id="cfdac-226">Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Deny log on through Remote Desktop Services</span></span>


8. <span data-ttu-id="cfdac-227">重新啟動 VM，以確保 Windows 仍然狀況良好，可使用 RDP 連線來達成。</span><span class="sxs-lookup"><span data-stu-id="cfdac-227">Restart the VM to make sure that Windows is still healthy can be reached by using the RDP connection.</span></span> <span data-ttu-id="cfdac-228">此時，您可能想要在本機 Hyper-V 中建立 VM，以確定 VM 已完全啟動，然後測試是否可連線到 RDP。</span><span class="sxs-lookup"><span data-stu-id="cfdac-228">At this point, you may want to create a VM in your local Hyper-V to make sure the VM is starting completely and then test whether it is RDP reachable.</span></span>

9. <span data-ttu-id="cfdac-229">移除任何額外的傳輸驅動程式介面篩選，例如分析 TCP 封包的軟體或額外的防火牆。</span><span class="sxs-lookup"><span data-stu-id="cfdac-229">Remove any extra Transport Driver Interface filters, such as software that analyzes TCP packets or extra firewalls.</span></span> <span data-ttu-id="cfdac-230">您也可以視需要，在 Azure 中部署 VM 之後的後續階段中檢閱這部分。</span><span class="sxs-lookup"><span data-stu-id="cfdac-230">You can also review this on a later stage after the VM is deployed in Azure if needed.</span></span>

10. <span data-ttu-id="cfdac-231">解除安裝與實體元件或任何其他虛擬化技術相關的所有其他協力廠商軟體和驅動程式。</span><span class="sxs-lookup"><span data-stu-id="cfdac-231">Uninstall any other third-party software and driver that is related to physical components or any other virtualization technology.</span></span>

### <a name="install-windows-updates"></a><span data-ttu-id="cfdac-232">安裝 Windows 更新</span><span class="sxs-lookup"><span data-stu-id="cfdac-232">Install Windows Updates</span></span>
<span data-ttu-id="cfdac-233">理想的設定是**具有最新的電腦修補程式等級**。</span><span class="sxs-lookup"><span data-stu-id="cfdac-233">The ideal configuration is to **have the patch level of the machine at the latest**.</span></span> <span data-ttu-id="cfdac-234">如果這不可行，請確定已安裝下列更新：</span><span class="sxs-lookup"><span data-stu-id="cfdac-234">If this is not possible, make sure that the following updates are installed:</span></span>

|                       |                   |           |                                       <span data-ttu-id="cfdac-235">最低檔案版本 x64</span><span class="sxs-lookup"><span data-stu-id="cfdac-235">Minimum file version x64</span></span>       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| <span data-ttu-id="cfdac-236">元件</span><span class="sxs-lookup"><span data-stu-id="cfdac-236">Component</span></span>               | <span data-ttu-id="cfdac-237">Binary</span><span class="sxs-lookup"><span data-stu-id="cfdac-237">Binary</span></span>            | <span data-ttu-id="cfdac-238">Windows 7 & Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cfdac-238">Windows 7 & Windows Server 2008 R2</span></span> | <span data-ttu-id="cfdac-239">Windows 8 & Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cfdac-239">Windows 8 & Windows Server 2012</span></span>             | <span data-ttu-id="cfdac-240">Windows 8.1 & Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cfdac-240">Windows 8.1 & Windows Server 2012 R2</span></span> | <span data-ttu-id="cfdac-241">Windows 10 & Windows Server 2016 RS1</span><span class="sxs-lookup"><span data-stu-id="cfdac-241">Windows 10 & Windows Server 2016 RS1</span></span> | <span data-ttu-id="cfdac-242">Windows 10 RS2</span><span class="sxs-lookup"><span data-stu-id="cfdac-242">Windows 10 RS2</span></span>             |
| <span data-ttu-id="cfdac-243">儲存體</span><span class="sxs-lookup"><span data-stu-id="cfdac-243">Storage</span></span>                 | <span data-ttu-id="cfdac-244">disk.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-244">disk.sys</span></span>          | <span data-ttu-id="cfdac-245">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-245">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="cfdac-246">6.2.9200.17638 / 6.2.9200.21757 - KB3137061</span></span> | <span data-ttu-id="cfdac-247">6.3.9600.18203 - KB3137061</span><span class="sxs-lookup"><span data-stu-id="cfdac-247">6.3.9600.18203 - KB3137061</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="cfdac-248">storport.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-248">storport.sys</span></span>      | <span data-ttu-id="cfdac-249">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-249">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span><span class="sxs-lookup"><span data-stu-id="cfdac-250">6.2.9200.17188 / 6.2.9200.21306 - KB3018489</span></span> | <span data-ttu-id="cfdac-251">6.3.9600.18573 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-251">6.3.9600.18573 - KB4022726</span></span>           | <span data-ttu-id="cfdac-252">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-252">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="cfdac-253">10.0.15063.332</span><span class="sxs-lookup"><span data-stu-id="cfdac-253">10.0.15063.332</span></span>             |
|                         | <span data-ttu-id="cfdac-254">ntfs.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-254">ntfs.sys</span></span>          | <span data-ttu-id="cfdac-255">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-255">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span><span class="sxs-lookup"><span data-stu-id="cfdac-256">6.2.9200.17623 / 6.2.9200.21743 - KB3121255</span></span> | <span data-ttu-id="cfdac-257">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-257">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="cfdac-258">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-258">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="cfdac-259">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="cfdac-259">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="cfdac-260">Iologmsg.dll</span><span class="sxs-lookup"><span data-stu-id="cfdac-260">Iologmsg.dll</span></span>      | <span data-ttu-id="cfdac-261">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-261">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-262">6.2.9200.16384 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="cfdac-262">6.2.9200.16384 - KB2995387</span></span>                  | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="cfdac-263">Classpnp.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-263">Classpnp.sys</span></span>      | <span data-ttu-id="cfdac-264">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-264">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span><span class="sxs-lookup"><span data-stu-id="cfdac-265">6.2.9200.17061 / 6.2.9200.21180 - KB2995387</span></span> | <span data-ttu-id="cfdac-266">6.3.9600.18334 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="cfdac-266">6.3.9600.18334 - KB3172614</span></span>           | <span data-ttu-id="cfdac-267">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-267">10.0.14393.953 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="cfdac-268">Volsnap.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-268">Volsnap.sys</span></span>       | <span data-ttu-id="cfdac-269">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-269">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span><span class="sxs-lookup"><span data-stu-id="cfdac-270">6.2.9200.17047 / 6.2.9200.21165 - KB2975331</span></span> | <span data-ttu-id="cfdac-271">6.3.9600.18265 - KB3145384</span><span class="sxs-lookup"><span data-stu-id="cfdac-271">6.3.9600.18265 - KB3145384</span></span>           | -                                    | <span data-ttu-id="cfdac-272">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-272">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-273">partmgr.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-273">partmgr.sys</span></span>       | <span data-ttu-id="cfdac-274">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-274">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-275">6.2.9200.16681 - KB2877114</span><span class="sxs-lookup"><span data-stu-id="cfdac-275">6.2.9200.16681 - KB2877114</span></span>                  | <span data-ttu-id="cfdac-276">6.3.9600.17401 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="cfdac-276">6.3.9600.17401 - KB3000850</span></span>           | <span data-ttu-id="cfdac-277">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-277">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="cfdac-278">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-278">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-279">volmgr.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-279">volmgr.sys</span></span>        |                                    |                                             |                                      |                                      | <span data-ttu-id="cfdac-280">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-280">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-281">Volmgrx.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-281">Volmgrx.sys</span></span>       | <span data-ttu-id="cfdac-282">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-282">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | <span data-ttu-id="cfdac-283">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-283">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-284">Msiscsi.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-284">Msiscsi.sys</span></span>       | <span data-ttu-id="cfdac-285">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-285">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-286">6.2.9200.21006 - KB2955163</span><span class="sxs-lookup"><span data-stu-id="cfdac-286">6.2.9200.21006 - KB2955163</span></span>                  | <span data-ttu-id="cfdac-287">6.3.9600.18624 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-287">6.3.9600.18624 - KB4022726</span></span>           | <span data-ttu-id="cfdac-288">10.0.14393.1066 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-288">10.0.14393.1066 - KB4022715</span></span>          | <span data-ttu-id="cfdac-289">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="cfdac-289">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="cfdac-290">Msdsm.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-290">Msdsm.sys</span></span>         | <span data-ttu-id="cfdac-291">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-291">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-292">6.2.9200.21474 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="cfdac-292">6.2.9200.21474 - KB3046101</span></span>                  | <span data-ttu-id="cfdac-293">6.3.9600.18592 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-293">6.3.9600.18592 - KB4022726</span></span>           | -                                    | -                          |
|                         | <span data-ttu-id="cfdac-294">Mpio.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-294">Mpio.sys</span></span>          | <span data-ttu-id="cfdac-295">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-295">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-296">6.2.9200.21190 - KB3046101</span><span class="sxs-lookup"><span data-stu-id="cfdac-296">6.2.9200.21190 - KB3046101</span></span>                  | <span data-ttu-id="cfdac-297">6.3.9600.18616 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-297">6.3.9600.18616 - KB4022726</span></span>           | <span data-ttu-id="cfdac-298">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-298">10.0.14393.1198 - KB4022715</span></span>          | -                          |
|                         | <span data-ttu-id="cfdac-299">Fveapi.dll</span><span class="sxs-lookup"><span data-stu-id="cfdac-299">Fveapi.dll</span></span>        | <span data-ttu-id="cfdac-300">6.1.7601.23311 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-300">6.1.7601.23311 - KB3125574</span></span>         | <span data-ttu-id="cfdac-301">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="cfdac-301">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="cfdac-302">6.3.9600.18294 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="cfdac-302">6.3.9600.18294 - KB3172614</span></span>           | <span data-ttu-id="cfdac-303">10.0.14393.576 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-303">10.0.14393.576 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="cfdac-304">Fveapibase.dll</span><span class="sxs-lookup"><span data-stu-id="cfdac-304">Fveapibase.dll</span></span>    | <span data-ttu-id="cfdac-305">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-305">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-306">6.2.9200.20930 - KB2930244</span><span class="sxs-lookup"><span data-stu-id="cfdac-306">6.2.9200.20930 - KB2930244</span></span>                  | <span data-ttu-id="cfdac-307">6.3.9600.17415 - KB3172614</span><span class="sxs-lookup"><span data-stu-id="cfdac-307">6.3.9600.17415 - KB3172614</span></span>           | <span data-ttu-id="cfdac-308">10.0.14393.206 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-308">10.0.14393.206 - KB4022715</span></span>           | -                          |
| <span data-ttu-id="cfdac-309">網路</span><span class="sxs-lookup"><span data-stu-id="cfdac-309">Network</span></span>                 | <span data-ttu-id="cfdac-310">netvsc.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-310">netvsc.sys</span></span>        | -                                  | -                                           | -                                    | <span data-ttu-id="cfdac-311">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-311">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="cfdac-312">10.0.15063.250 - KB4020001</span><span class="sxs-lookup"><span data-stu-id="cfdac-312">10.0.15063.250 - KB4020001</span></span> |
|                         | <span data-ttu-id="cfdac-313">mrxsmb10.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-313">mrxsmb10.sys</span></span>      | <span data-ttu-id="cfdac-314">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="cfdac-314">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="cfdac-315">6.2.9200.22108 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="cfdac-315">6.2.9200.22108 - KB4022724</span></span>                  | <span data-ttu-id="cfdac-316">6.3.9600.18603 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-316">6.3.9600.18603 - KB4022726</span></span>           | <span data-ttu-id="cfdac-317">10.0.14393.479 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-317">10.0.14393.479 - KB4022715</span></span>           | <span data-ttu-id="cfdac-318">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="cfdac-318">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="cfdac-319">mrxsmb20.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-319">mrxsmb20.sys</span></span>      | <span data-ttu-id="cfdac-320">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="cfdac-320">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="cfdac-321">6.2.9200.21548 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="cfdac-321">6.2.9200.21548 - KB4022724</span></span>                  | <span data-ttu-id="cfdac-322">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-322">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="cfdac-323">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-323">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="cfdac-324">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="cfdac-324">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="cfdac-325">mrxsmb.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-325">mrxsmb.sys</span></span>        | <span data-ttu-id="cfdac-326">6.1.7601.23816 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="cfdac-326">6.1.7601.23816 - KB4022722</span></span>         | <span data-ttu-id="cfdac-327">6.2.9200.22074 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="cfdac-327">6.2.9200.22074 - KB4022724</span></span>                  | <span data-ttu-id="cfdac-328">6.3.9600.18586 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-328">6.3.9600.18586 - KB4022726</span></span>           | <span data-ttu-id="cfdac-329">10.0.14393.953 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-329">10.0.14393.953 - KB4022715</span></span>           | <span data-ttu-id="cfdac-330">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-330">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-331">tcpip.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-331">tcpip.sys</span></span>         | <span data-ttu-id="cfdac-332">6.1.7601.23761 - KB4022722</span><span class="sxs-lookup"><span data-stu-id="cfdac-332">6.1.7601.23761 - KB4022722</span></span>         | <span data-ttu-id="cfdac-333">6.2.9200.22070 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="cfdac-333">6.2.9200.22070 - KB4022724</span></span>                  | <span data-ttu-id="cfdac-334">6.3.9600.18478 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-334">6.3.9600.18478 - KB4022726</span></span>           | <span data-ttu-id="cfdac-335">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-335">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="cfdac-336">10.0.15063.447</span><span class="sxs-lookup"><span data-stu-id="cfdac-336">10.0.15063.447</span></span>             |
|                         | <span data-ttu-id="cfdac-337">http.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-337">http.sys</span></span>          | <span data-ttu-id="cfdac-338">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-338">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-339">6.2.9200.17285 - KB3042553</span><span class="sxs-lookup"><span data-stu-id="cfdac-339">6.2.9200.17285 - KB3042553</span></span>                  | <span data-ttu-id="cfdac-340">6.3.9600.18574 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-340">6.3.9600.18574 - KB4022726</span></span>           | <span data-ttu-id="cfdac-341">10.0.14393.251 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-341">10.0.14393.251 - KB4022715</span></span>           | <span data-ttu-id="cfdac-342">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="cfdac-342">10.0.15063.483</span></span>             |
|                         | <span data-ttu-id="cfdac-343">vmswitch.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-343">vmswitch.sys</span></span>      | <span data-ttu-id="cfdac-344">6.1.7601.23727 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="cfdac-344">6.1.7601.23727 - KB4022719</span></span>         | <span data-ttu-id="cfdac-345">6.2.9200.22117 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="cfdac-345">6.2.9200.22117 - KB4022724</span></span>                  | <span data-ttu-id="cfdac-346">6.3.9600.18654 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-346">6.3.9600.18654 - KB4022726</span></span>           | <span data-ttu-id="cfdac-347">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-347">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="cfdac-348">10.0.15063.138</span><span class="sxs-lookup"><span data-stu-id="cfdac-348">10.0.15063.138</span></span>             |
| <span data-ttu-id="cfdac-349">核心</span><span class="sxs-lookup"><span data-stu-id="cfdac-349">Core</span></span>                    | <span data-ttu-id="cfdac-350">ntoskrnl.exe</span><span class="sxs-lookup"><span data-stu-id="cfdac-350">ntoskrnl.exe</span></span>      | <span data-ttu-id="cfdac-351">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="cfdac-351">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="cfdac-352">6.2.9200.22170 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="cfdac-352">6.2.9200.22170 - KB4022718</span></span>                  | <span data-ttu-id="cfdac-353">6.3.9600.18696 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-353">6.3.9600.18696 - KB4022726</span></span>           | <span data-ttu-id="cfdac-354">10.0.14393.1358 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-354">10.0.14393.1358 - KB4022715</span></span>          | <span data-ttu-id="cfdac-355">10.0.15063.483</span><span class="sxs-lookup"><span data-stu-id="cfdac-355">10.0.15063.483</span></span>             |
| <span data-ttu-id="cfdac-356">遠端桌面服務問題</span><span class="sxs-lookup"><span data-stu-id="cfdac-356">Remote Desktop Services</span></span> | <span data-ttu-id="cfdac-357">rdpcorets.dll</span><span class="sxs-lookup"><span data-stu-id="cfdac-357">rdpcorets.dll</span></span>     | <span data-ttu-id="cfdac-358">6.2.9200.21506 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="cfdac-358">6.2.9200.21506 - KB4022719</span></span>         | <span data-ttu-id="cfdac-359">6.2.9200.22104 - KB4022724</span><span class="sxs-lookup"><span data-stu-id="cfdac-359">6.2.9200.22104 - KB4022724</span></span>                  | <span data-ttu-id="cfdac-360">6.3.9600.18619 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-360">6.3.9600.18619 - KB4022726</span></span>           | <span data-ttu-id="cfdac-361">10.0.14393.1198 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-361">10.0.14393.1198 - KB4022715</span></span>          | <span data-ttu-id="cfdac-362">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-362">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-363">termsrv.dll</span><span class="sxs-lookup"><span data-stu-id="cfdac-363">termsrv.dll</span></span>       | <span data-ttu-id="cfdac-364">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-364">6.1.7601.23403 - KB3125574</span></span>         | <span data-ttu-id="cfdac-365">6.2.9200.17048 - KB2973501</span><span class="sxs-lookup"><span data-stu-id="cfdac-365">6.2.9200.17048 - KB2973501</span></span>                  | <span data-ttu-id="cfdac-366">6.3.9600.17415 - KB3000850</span><span class="sxs-lookup"><span data-stu-id="cfdac-366">6.3.9600.17415 - KB3000850</span></span>           | <span data-ttu-id="cfdac-367">10.0.14393.0 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-367">10.0.14393.0 - KB4022715</span></span>             | <span data-ttu-id="cfdac-368">10.0.15063.0</span><span class="sxs-lookup"><span data-stu-id="cfdac-368">10.0.15063.0</span></span>               |
|                         | <span data-ttu-id="cfdac-369">termdd.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-369">termdd.sys</span></span>        | <span data-ttu-id="cfdac-370">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-370">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="cfdac-371">win32k.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-371">win32k.sys</span></span>        | <span data-ttu-id="cfdac-372">6.1.7601.23807 - KB4022719</span><span class="sxs-lookup"><span data-stu-id="cfdac-372">6.1.7601.23807 - KB4022719</span></span>         | <span data-ttu-id="cfdac-373">6.2.9200.22168 - KB4022718</span><span class="sxs-lookup"><span data-stu-id="cfdac-373">6.2.9200.22168 - KB4022718</span></span>                  | <span data-ttu-id="cfdac-374">6.3.9600.18698 - KB4022726</span><span class="sxs-lookup"><span data-stu-id="cfdac-374">6.3.9600.18698 - KB4022726</span></span>           | <span data-ttu-id="cfdac-375">10.0.14393.594 - KB4022715</span><span class="sxs-lookup"><span data-stu-id="cfdac-375">10.0.14393.594 - KB4022715</span></span>           | -                          |
|                         | <span data-ttu-id="cfdac-376">rdpdd.dll</span><span class="sxs-lookup"><span data-stu-id="cfdac-376">rdpdd.dll</span></span>         | <span data-ttu-id="cfdac-377">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-377">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
|                         | <span data-ttu-id="cfdac-378">rdpwd.sys</span><span class="sxs-lookup"><span data-stu-id="cfdac-378">rdpwd.sys</span></span>         | <span data-ttu-id="cfdac-379">6.1.7601.23403 - KB3125574</span><span class="sxs-lookup"><span data-stu-id="cfdac-379">6.1.7601.23403 - KB3125574</span></span>         | -                                           | -                                    | -                                    | -                          |
| <span data-ttu-id="cfdac-380">安全性</span><span class="sxs-lookup"><span data-stu-id="cfdac-380">Security</span></span>                | <span data-ttu-id="cfdac-381">預定 WannaCrypt</span><span class="sxs-lookup"><span data-stu-id="cfdac-381">Due to WannaCrypt</span></span> | <span data-ttu-id="cfdac-382">KB4012212</span><span class="sxs-lookup"><span data-stu-id="cfdac-382">KB4012212</span></span>                          | <span data-ttu-id="cfdac-383">KB4012213</span><span class="sxs-lookup"><span data-stu-id="cfdac-383">KB4012213</span></span>                                   | <span data-ttu-id="cfdac-384">KB4012213</span><span class="sxs-lookup"><span data-stu-id="cfdac-384">KB4012213</span></span>                            | <span data-ttu-id="cfdac-385">KB4012606</span><span class="sxs-lookup"><span data-stu-id="cfdac-385">KB4012606</span></span>                            | <span data-ttu-id="cfdac-386">KB4012606</span><span class="sxs-lookup"><span data-stu-id="cfdac-386">KB4012606</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="cfdac-387">KB4012216</span><span class="sxs-lookup"><span data-stu-id="cfdac-387">KB4012216</span></span>                                   |                                      | <span data-ttu-id="cfdac-388">KB4013198</span><span class="sxs-lookup"><span data-stu-id="cfdac-388">KB4013198</span></span>                            | <span data-ttu-id="cfdac-389">KB4013198</span><span class="sxs-lookup"><span data-stu-id="cfdac-389">KB4013198</span></span>                  |
|                         |                   | <span data-ttu-id="cfdac-390">KB4012215</span><span class="sxs-lookup"><span data-stu-id="cfdac-390">KB4012215</span></span>                          | <span data-ttu-id="cfdac-391">KB4012214</span><span class="sxs-lookup"><span data-stu-id="cfdac-391">KB4012214</span></span>                                   | <span data-ttu-id="cfdac-392">KB4012216</span><span class="sxs-lookup"><span data-stu-id="cfdac-392">KB4012216</span></span>                            | <span data-ttu-id="cfdac-393">KB4013429</span><span class="sxs-lookup"><span data-stu-id="cfdac-393">KB4013429</span></span>                            | <span data-ttu-id="cfdac-394">KB4013429</span><span class="sxs-lookup"><span data-stu-id="cfdac-394">KB4013429</span></span>                  |
|                         |                   |                                    | <span data-ttu-id="cfdac-395">KB4012217</span><span class="sxs-lookup"><span data-stu-id="cfdac-395">KB4012217</span></span>                                   |                                      | <span data-ttu-id="cfdac-396">KB4013429</span><span class="sxs-lookup"><span data-stu-id="cfdac-396">KB4013429</span></span>                            | <span data-ttu-id="cfdac-397">KB4013429</span><span class="sxs-lookup"><span data-stu-id="cfdac-397">KB4013429</span></span>                  |
       
### <span data-ttu-id="cfdac-398">使用 sysprep 的時機 <a id="step23"></a></span><span class="sxs-lookup"><span data-stu-id="cfdac-398">When to use sysprep <a id="step23"></a></span></span>    

<span data-ttu-id="cfdac-399">Sysprep 是您可執行來進行 Windows 安裝的程序，將重設系統安裝，且將藉由移除所有個人資料並重設數個元件來提供「全新體驗」。</span><span class="sxs-lookup"><span data-stu-id="cfdac-399">Sysprep is a process that you could run into a windows installation that will reset the installation of the system and will provide an “out of the box experience” by removing all personal data and resetting several components.</span></span> <span data-ttu-id="cfdac-400">如果您想要建立一個範本，以部署數個其他具有特定設定的 VM，通常會執行此動作。</span><span class="sxs-lookup"><span data-stu-id="cfdac-400">You typically do this if you want to create a template from which you can deploy several other VMs that have a specific configuration.</span></span> <span data-ttu-id="cfdac-401">這稱為**一般化映像**。</span><span class="sxs-lookup"><span data-stu-id="cfdac-401">This is called a **generalized image**.</span></span>

<span data-ttu-id="cfdac-402">但若您只想從一部磁碟建立一個 VM，就不需使用 sysprep。</span><span class="sxs-lookup"><span data-stu-id="cfdac-402">If, instead, you want only to create one VM from one disk, you don’t have to use sysprep.</span></span> <span data-ttu-id="cfdac-403">在此情況下，您只需從所謂的**特殊化映像**建立 VM 即可。</span><span class="sxs-lookup"><span data-stu-id="cfdac-403">In this situation, you can just create the VM from what is known as a **specialized image**.</span></span>

<span data-ttu-id="cfdac-404">如需如何從特殊化磁碟建立 VM 的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="cfdac-404">For more information about how to create a VM from a specialized disk, see:</span></span>

- [<span data-ttu-id="cfdac-405">從特殊化磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="cfdac-405">Create a VM from a specialized disk</span></span>](create-vm-specialized.md)
- [<span data-ttu-id="cfdac-406">從特殊化 VHD 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="cfdac-406">Create a VM from a specialized VHD disk</span></span>](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

<span data-ttu-id="cfdac-407">如果您想要建立一般化映像，就必須執行 sysprep。</span><span class="sxs-lookup"><span data-stu-id="cfdac-407">If you want to create a generalized image, you need to run sysprep.</span></span> <span data-ttu-id="cfdac-408">如需 Sysprep 的詳細資訊，請參閱[如何使用 Sysprep：簡介](http://technet.microsoft.com/library/bb457073.aspx) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-408">For more information about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> 

<span data-ttu-id="cfdac-409">並非 Windows 電腦上安裝的每個角色或應用程式都支援這個一般化。</span><span class="sxs-lookup"><span data-stu-id="cfdac-409">Not every role or application that’s installed on a Windows-based computer supports this generalization.</span></span> <span data-ttu-id="cfdac-410">因此，在執行此程序之前，請先參閱下列文章，以確定 sysprep 支援該電腦的角色。</span><span class="sxs-lookup"><span data-stu-id="cfdac-410">So before you run this procedure, refer to the following article to make sure that the role of that computer is supported by sysprep.</span></span> <span data-ttu-id="cfdac-411">如需詳細資訊，請參閱[伺服器角色的 Sysprep 支援](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-411">For more information, [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

### <a name="steps-to-generalize-a-vhd"></a><span data-ttu-id="cfdac-412">將 VHD 一般化的步驟</span><span class="sxs-lookup"><span data-stu-id="cfdac-412">Steps to generalize a VHD</span></span>

>[!NOTE]
> <span data-ttu-id="cfdac-413">當您執行 sysprep.exe 之後 (如下列步驟中所指定)，請關閉 VM，且在您於 Azure 中建立它的映像之前，不要再度開啟它。</span><span class="sxs-lookup"><span data-stu-id="cfdac-413">After you run sysprep.exe as specified  in the following steps, turn off the VM, and do not turn it back on until you create an image from it in Azure.</span></span>

1. <span data-ttu-id="cfdac-414">登入 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-414">Sign in to the Windows VM.</span></span>
2. <span data-ttu-id="cfdac-415">以系統管理員身分執行**命令提示字元**。</span><span class="sxs-lookup"><span data-stu-id="cfdac-415">Run **Command Prompt** as an administrator.</span></span> 
3. <span data-ttu-id="cfdac-416">將目錄切換至：**%windir%\system32\sysprep**，然後執行 **sysprep.exe**。</span><span class="sxs-lookup"><span data-stu-id="cfdac-416">Change the directory to: **%windir%\system32\sysprep**, and then run **sysprep.exe**.</span></span>
3. <span data-ttu-id="cfdac-417">在 [系統準備工具] 對話方塊中，選取 [進入系統全新體驗 (OOBE)]，並確認已勾選 [一般化] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cfdac-417">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>

    ![系統準備工具](media/prepare-for-upload-vhd-image/syspre.png)
4. <span data-ttu-id="cfdac-419">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="cfdac-419">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="cfdac-420">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cfdac-420">Click **OK**.</span></span>
6. <span data-ttu-id="cfdac-421">當 Sysprep 完成時，關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-421">When Sysprep completes, shut down the VM.</span></span> <span data-ttu-id="cfdac-422">不要使用**重新啟動**來關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="cfdac-422">Do not use **Restart** to shut down the VM.</span></span>
7. <span data-ttu-id="cfdac-423">現在已準備好上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="cfdac-423">Now the VHD is ready to be uploaded.</span></span> <span data-ttu-id="cfdac-424">如需如何從一般化磁碟建立 VM 的詳細資訊，請參閱[將一般化 VHD 上傳，並使用它在 Azure 中建立新的 VM](sa-upload-generalized.md)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-424">For more information about how to create a VM from a generalized disk, see [Upload a generalized VHD and use it to create a new VMs in Azure](sa-upload-generalized.md).</span></span>


## <a name="complete-recommended-configurations"></a><span data-ttu-id="cfdac-425">完成建議的設定</span><span class="sxs-lookup"><span data-stu-id="cfdac-425">Complete recommended configurations</span></span>
<span data-ttu-id="cfdac-426">下列設定不會影響 VHD 上傳。</span><span class="sxs-lookup"><span data-stu-id="cfdac-426">The following settings do not affect VHD uploading.</span></span> <span data-ttu-id="cfdac-427">不過，我們強烈建議您設定它們。</span><span class="sxs-lookup"><span data-stu-id="cfdac-427">However, we strongly recommend that you configured them.</span></span>

* <span data-ttu-id="cfdac-428">安裝 [Azure VM 代理程式](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="cfdac-428">Install the [Azure VMs Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="cfdac-429">然後您可以啟用 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="cfdac-429">Then you can enable VM extensions.</span></span> <span data-ttu-id="cfdac-430">VM 擴充功能實作了您可能想要與 VM 搭配使用的大部分重要功能，例如重設密碼、設定 RDP 等功能。</span><span class="sxs-lookup"><span data-stu-id="cfdac-430">The VM extensions implement most of the critical functionality that you might want to use with your VMs such as resetting passwords, configuring RDP, and so on.</span></span> <span data-ttu-id="cfdac-431">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="cfdac-431">For more information, see:</span></span>

    - <span data-ttu-id="cfdac-432">[VM 代理程式與擴充功能 - 第 1 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="cfdac-432">[VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)</span></span>
    - <span data-ttu-id="cfdac-433">[VM 代理程式與擴充功能 - 第 2 部分](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="cfdac-433">[VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)</span></span>
* <span data-ttu-id="cfdac-434">傾印記錄檔能幫助您進行 Windows 損毀問題的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="cfdac-434">The Dump log can be helpful in troubleshooting Windows crash issues.</span></span> <span data-ttu-id="cfdac-435">啟用傾印記錄檔收集：</span><span class="sxs-lookup"><span data-stu-id="cfdac-435">Enable the Dump log collection:</span></span>
  
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
    <span data-ttu-id="cfdac-436">如果您在本文的任一個程序步驟中收到任何錯誤，這表示登錄機碼已經存在。</span><span class="sxs-lookup"><span data-stu-id="cfdac-436">If you receive any errors during any of the procedural steps in this article, this means that the registry keys already exists.</span></span> <span data-ttu-id="cfdac-437">在此情況下，請改用下列命令：</span><span class="sxs-lookup"><span data-stu-id="cfdac-437">In this situation, use the following commands instead:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  <span data-ttu-id="cfdac-438">在 Azure 中建立 VM 之後，我們建議您將分頁檔放在「暫存磁碟機」磁碟區中，以改善效能。</span><span class="sxs-lookup"><span data-stu-id="cfdac-438">After the VM is created in Azure, we recommend that you put the pagefile on the ”Temporal drive” volume to improve performance.</span></span> <span data-ttu-id="cfdac-439">您可以如下方式設定這部分：</span><span class="sxs-lookup"><span data-stu-id="cfdac-439">You can set up this as follows:</span></span>

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
<span data-ttu-id="cfdac-440">如果沒有任何資料磁碟連接到 VM，暫存磁碟機磁碟區的磁碟機代號通常是 "D"。</span><span class="sxs-lookup"><span data-stu-id="cfdac-440">If there’s any data disk that is attached to the VM, the Temporal drive volume's drive letter is typically "D."</span></span> <span data-ttu-id="cfdac-441">根據可用的磁碟機數目和您所進行的設定而定，這項指定可能不同。</span><span class="sxs-lookup"><span data-stu-id="cfdac-441">This designation could be different, depending on the number of available drives and the settings that you  make.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfdac-442">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfdac-442">Next steps</span></span>
* [<span data-ttu-id="cfdac-443">將 Windows VM 映像上傳至 Azure 供 Resource Manager 部署使用</span><span class="sxs-lookup"><span data-stu-id="cfdac-443">Upload a Windows VM image to Azure for Resource Manager deployments</span></span>](upload-generalized-managed.md)


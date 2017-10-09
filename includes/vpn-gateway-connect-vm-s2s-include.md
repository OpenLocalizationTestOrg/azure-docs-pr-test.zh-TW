<span data-ttu-id="46dc1-101">您可以連接 tooa 是已部署的 tooyour VNet 建立遠端桌面連線 tooyour VM 的 VM。</span><span class="sxs-lookup"><span data-stu-id="46dc1-101">You can connect tooa VM that is deployed tooyour VNet by creating a Remote Desktop Connection tooyour VM.</span></span> <span data-ttu-id="46dc1-102">hello 最佳方式 tooinitially 確認您可以連線的 VM 是由 tooconnect tooyour 使用其私人 IP 位址，而非電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="46dc1-102">hello best way tooinitially verify that you can connect tooyour VM is tooconnect by using its private IP address, rather than computer name.</span></span> <span data-ttu-id="46dc1-103">這樣一來，您要測試 toosee 如果您可以連接，不是否名稱解析設定正確。</span><span class="sxs-lookup"><span data-stu-id="46dc1-103">That way, you are testing toosee if you can connect, not whether name resolution is configured properly.</span></span>

1. <span data-ttu-id="46dc1-104">找出 hello 私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="46dc1-104">Locate hello private IP address.</span></span> <span data-ttu-id="46dc1-105">您可以用多種方式找到 VM 的 hello 私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="46dc1-105">You can find hello private IP address of a VM in multiple ways.</span></span> <span data-ttu-id="46dc1-106">以下，我們會顯示 hello 步驟 hello Azure 入口網站和 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="46dc1-106">Below, we show hello steps for hello Azure portal and for PowerShell.</span></span>

  - <span data-ttu-id="46dc1-107">Azure 入口網站位在 hello Azure 入口網站中尋找您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="46dc1-107">Azure portal - Locate your virtual machine in hello Azure portal.</span></span> <span data-ttu-id="46dc1-108">檢視 hello hello VM 的屬性。</span><span class="sxs-lookup"><span data-stu-id="46dc1-108">View hello properties for hello VM.</span></span> <span data-ttu-id="46dc1-109">會列出 hello 私用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="46dc1-109">hello private IP address is listed.</span></span>

  - <span data-ttu-id="46dc1-110">PowerShell-使用 hello 範例 tooview Vm 和私人 IP 位址，從資源群組的清單。</span><span class="sxs-lookup"><span data-stu-id="46dc1-110">PowerShell - Use hello example tooview a list of VMs and private IP addresses from your resource groups.</span></span> <span data-ttu-id="46dc1-111">您不需要 toomodify 此範例中，再使用它。</span><span class="sxs-lookup"><span data-stu-id="46dc1-111">You don't need toomodify this example before using it.</span></span>

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. <span data-ttu-id="46dc1-112">確認您是否已連線的 tooyour VNet 使用 hello VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="46dc1-112">Verify that you are connected tooyour VNet using hello VPN connection.</span></span>
3. <span data-ttu-id="46dc1-113">開啟**遠端桌面連線**hello hello 工作列上的搜尋方塊中輸入"RDP 」 或 「 遠端桌面連線 」，然後選取 遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="46dc1-113">Open **Remote Desktop Connection** by typing "RDP" or "Remote Desktop Connection" in hello search box on hello taskbar, then select Remote Desktop Connection.</span></span> <span data-ttu-id="46dc1-114">您也可以開啟 遠端桌面連線在 PowerShell 中使用 hello 'mstsc' 命令。</span><span class="sxs-lookup"><span data-stu-id="46dc1-114">You can also open Remote Desktop Connection using hello 'mstsc' command in PowerShell.</span></span> 
4. <span data-ttu-id="46dc1-115">在遠端桌面連線中，輸入 hello VM 的 hello 私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="46dc1-115">In Remote Desktop Connection, enter hello private IP address of hello VM.</span></span> <span data-ttu-id="46dc1-116">您可以按一下 [顯示選項] tooadjust 其他設定，然後連接。</span><span class="sxs-lookup"><span data-stu-id="46dc1-116">You can click "Show Options" tooadjust additional settings, then connect.</span></span>

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a><span data-ttu-id="46dc1-117">tootroubleshoot RDP 連線 tooa VM</span><span class="sxs-lookup"><span data-stu-id="46dc1-117">tootroubleshoot an RDP connection tooa VM</span></span>

<span data-ttu-id="46dc1-118">如果您無法透過 VPN 連線連線 tooa 虛擬機器，請檢查 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="46dc1-118">If you are having trouble connecting tooa virtual machine over your VPN connection, check hello following:</span></span>

- <span data-ttu-id="46dc1-119">確認您的 VPN 連線成功。</span><span class="sxs-lookup"><span data-stu-id="46dc1-119">Verify that your VPN connection is successful.</span></span>
- <span data-ttu-id="46dc1-120">請確認您所連接的 hello VM toohello 私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="46dc1-120">Verify that you are connecting toohello private IP address for hello VM.</span></span>
- <span data-ttu-id="46dc1-121">如果您可以連接 toohello VM 使用 hello 私人 IP 位址，但不是 hello 電腦名稱，請確認已正確設定 DNS。</span><span class="sxs-lookup"><span data-stu-id="46dc1-121">If you can connect toohello VM using hello private IP address, but not hello computer name, verify that you have configured DNS properly.</span></span> <span data-ttu-id="46dc1-122">如需 VM 的名稱解析運作方式的詳細資訊，請參閱 [VM 的名稱解析](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="46dc1-122">For more information about how name resolution works for VMs, see [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
- <span data-ttu-id="46dc1-123">如需 RDP 連線的詳細資訊，請參閱[疑難排解遠端桌面連線 tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="46dc1-123">For more information about RDP connections, see [Troubleshoot Remote Desktop connections tooa VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).</span></span>

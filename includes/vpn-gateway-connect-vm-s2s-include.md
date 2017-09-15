<span data-ttu-id="65556-101">您可以建立 VM 的遠端桌面連線，以連線至已部署至 VNet 的 VM。</span><span class="sxs-lookup"><span data-stu-id="65556-101">You can connect to a VM that is deployed to your VNet by creating a Remote Desktop Connection to your VM.</span></span> <span data-ttu-id="65556-102">一開始確認您可以連線至 VM 的最佳方法是使用其私人 IP 位址 (而不是電腦名稱) 進行連線。</span><span class="sxs-lookup"><span data-stu-id="65556-102">The best way to initially verify that you can connect to your VM is to connect by using its private IP address, rather than computer name.</span></span> <span data-ttu-id="65556-103">這樣一來，您會測試以查看您是否可以連線，而不是否已正確設定名稱解析。</span><span class="sxs-lookup"><span data-stu-id="65556-103">That way, you are testing to see if you can connect, not whether name resolution is configured properly.</span></span>

1. <span data-ttu-id="65556-104">找出私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="65556-104">Locate the private IP address.</span></span> <span data-ttu-id="65556-105">您可以使用多種方法找到 VM 的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="65556-105">You can find the private IP address of a VM in multiple ways.</span></span> <span data-ttu-id="65556-106">以下，我們示範 Azure 入口網站和 PowerShell 適用的步驟。</span><span class="sxs-lookup"><span data-stu-id="65556-106">Below, we show the steps for the Azure portal and for PowerShell.</span></span>

  - <span data-ttu-id="65556-107">Azure 入口網站 - 在 Azure 入口網站中尋找您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="65556-107">Azure portal - Locate your virtual machine in the Azure portal.</span></span> <span data-ttu-id="65556-108">檢視 VM 的屬性。</span><span class="sxs-lookup"><span data-stu-id="65556-108">View the properties for the VM.</span></span> <span data-ttu-id="65556-109">系統會列出私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="65556-109">The private IP address is listed.</span></span>

  - <span data-ttu-id="65556-110">PowerShell - 使用範例來檢視資源群組中的 VM 和私人 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="65556-110">PowerShell - Use the example to view a list of VMs and private IP addresses from your resource groups.</span></span> <span data-ttu-id="65556-111">使用此範例前，您不需要加以修改。</span><span class="sxs-lookup"><span data-stu-id="65556-111">You don't need to modify this example before using it.</span></span>

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

2. <span data-ttu-id="65556-112">確認您已使用 VPN 連線來連線至 VNet。</span><span class="sxs-lookup"><span data-stu-id="65556-112">Verify that you are connected to your VNet using the VPN connection.</span></span>
3. <span data-ttu-id="65556-113">在工作列上的搜尋方塊中輸入「RDP」或「遠端桌面連線」以開啟遠端桌面連線，然後選取 [遠端桌面連線]。</span><span class="sxs-lookup"><span data-stu-id="65556-113">Open **Remote Desktop Connection** by typing "RDP" or "Remote Desktop Connection" in the search box on the taskbar, then select Remote Desktop Connection.</span></span> <span data-ttu-id="65556-114">您也可以使用 PowerShell 中的 'mstsc' 命令開啟遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="65556-114">You can also open Remote Desktop Connection using the 'mstsc' command in PowerShell.</span></span> 
4. <span data-ttu-id="65556-115">在 [遠端桌面連線] 中，輸入 VM 的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="65556-115">In Remote Desktop Connection, enter the private IP address of the VM.</span></span> <span data-ttu-id="65556-116">您可以按一下 [顯示選項] 來調整其他設定，然後進行連線。</span><span class="sxs-lookup"><span data-stu-id="65556-116">You can click "Show Options" to adjust additional settings, then connect.</span></span>

### <a name="to-troubleshoot-an-rdp-connection-to-a-vm"></a><span data-ttu-id="65556-117">針對 VM 的 RDP 連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="65556-117">To troubleshoot an RDP connection to a VM</span></span>

<span data-ttu-id="65556-118">如果您無法透過 VPN 連線與虛擬機器連線，請檢查下列各項：</span><span class="sxs-lookup"><span data-stu-id="65556-118">If you are having trouble connecting to a virtual machine over your VPN connection, check the following:</span></span>

- <span data-ttu-id="65556-119">確認您的 VPN 連線成功。</span><span class="sxs-lookup"><span data-stu-id="65556-119">Verify that your VPN connection is successful.</span></span>
- <span data-ttu-id="65556-120">確認您是連線至 VM 的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="65556-120">Verify that you are connecting to the private IP address for the VM.</span></span>
- <span data-ttu-id="65556-121">如果您可以使用私人 IP 位址 (而非電腦名稱) 來連線至 VM，請確認您已正確設定 DNS。</span><span class="sxs-lookup"><span data-stu-id="65556-121">If you can connect to the VM using the private IP address, but not the computer name, verify that you have configured DNS properly.</span></span> <span data-ttu-id="65556-122">如需 VM 的名稱解析運作方式的詳細資訊，請參閱 [VM 的名稱解析](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)。</span><span class="sxs-lookup"><span data-stu-id="65556-122">For more information about how name resolution works for VMs, see [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
- <span data-ttu-id="65556-123">如需 RDP 連線的詳細資訊，請參閱[針對 VM 的遠端桌面連線進行疑難排解](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="65556-123">For more information about RDP connections, see [Troubleshoot Remote Desktop connections to a VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).</span></span>
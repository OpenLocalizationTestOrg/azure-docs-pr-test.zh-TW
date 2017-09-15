## <span data-ttu-id="07593-101"><a name="os-config"></a>將 IP 位址新增至 VM 作業系統</span><span class="sxs-lookup"><span data-stu-id="07593-101"><a name="os-config"></a>Add IP addresses to a VM operating system</span></span>

<span data-ttu-id="07593-102">連接並登入您使用多個私人 IP 位址建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="07593-102">Connect and login to a VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="07593-103">您必須手動新增您新增至 VM 的所有私人 IP 位址 (包括主要位址)。</span><span class="sxs-lookup"><span data-stu-id="07593-103">You must manually add all the private IP addresses (including the primary) that you added to the VM.</span></span> <span data-ttu-id="07593-104">對您的 VM 作業系統完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="07593-104">Complete the following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="07593-105">Windows</span><span class="sxs-lookup"><span data-stu-id="07593-105">Windows</span></span>

1. <span data-ttu-id="07593-106">從命令提示字元輸入 *ipconfig /all*。</span><span class="sxs-lookup"><span data-stu-id="07593-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="07593-107">您只會看到 *Primary* 私人 IP 位址 (透過 DHCP)。</span><span class="sxs-lookup"><span data-stu-id="07593-107">You only see the *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="07593-108">在命令提示字元中輸入 ncpa.cpl，以開啟 [網路連線]。</span><span class="sxs-lookup"><span data-stu-id="07593-108">Type *ncpa.cpl* in the command prompt to open the **Network connections** window.</span></span>
3. <span data-ttu-id="07593-109">開啟適當介面卡的屬性：**區域連線**。</span><span class="sxs-lookup"><span data-stu-id="07593-109">Open the properties for the appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="07593-110">按兩下 [網際網路通訊協定第 4 版 (IPv4)]。</span><span class="sxs-lookup"><span data-stu-id="07593-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="07593-111">選取 [使用下列 IP 位址]  並輸入下列值︰</span><span class="sxs-lookup"><span data-stu-id="07593-111">Select **Use the following IP address** and enter the following values:</span></span>

    * <span data-ttu-id="07593-112">**IP 位址**︰輸入 *Primary* 私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="07593-112">**IP address**: Enter the *Primary* private IP address</span></span>
    * <span data-ttu-id="07593-113">**子網路遮罩**︰根據您的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="07593-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="07593-114">例如，如果子網路為 /24 子網路，則子網路遮罩為 255.255.255.0。</span><span class="sxs-lookup"><span data-stu-id="07593-114">For example, if the subnet is a /24 subnet then the subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="07593-115">**預設閘道**︰子網路中的第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07593-115">**Default gateway**: The first IP address in the subnet.</span></span> <span data-ttu-id="07593-116">如果您的子網路為 10.0.0.0/24，則閘道 IP 位址為 10.0.0.1。</span><span class="sxs-lookup"><span data-stu-id="07593-116">If your subnet is 10.0.0.0/24, then the gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="07593-117">按一下 [使用下列 DNS 伺服器位址]  並輸入下列值︰</span><span class="sxs-lookup"><span data-stu-id="07593-117">Click **Use the following DNS server addresses** and enter the following values:</span></span>
        * <span data-ttu-id="07593-118">**慣用 DNS 伺服器**︰如果您不是使用自己的 DNS 伺服器，請輸入 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="07593-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="07593-119">如果您是使用自己的 DNS 伺服器，請輸入您的伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07593-119">If you are using your own DNS server, enter the IP address for your server.</span></span>
    * <span data-ttu-id="07593-120">按一下 [進階]  按鈕，然後新增其他 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07593-120">Click the **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="07593-121">使用為主要 IP 位址指定時相同的子網路，對 NIC 新增步驟 8 中列出的每個次要私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07593-121">Add each of the secondary private IP addresses listed in step 8 to the NIC with the same subnet specified for the primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="07593-122">如果您未正確地遵循上述步驟，您的 VM 可能會中斷連線。</span><span class="sxs-lookup"><span data-stu-id="07593-122">If you do not follow the steps above correctly, you may lose connectivity to your VM.</span></span> <span data-ttu-id="07593-123">請先確定針對步驟 5 輸入的資訊正確無誤﹐再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="07593-123">Ensure the information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="07593-124">按一下 [確定] 關閉 TCP/IP 設定，然後再按一次 [確定] 關閉介面卡設定。</span><span class="sxs-lookup"><span data-stu-id="07593-124">Click **OK** to close out the TCP/IP settings and then **OK** again to close the adapter settings.</span></span> <span data-ttu-id="07593-125">您的 RDP 連接已重建。</span><span class="sxs-lookup"><span data-stu-id="07593-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="07593-126">從命令提示字元輸入 *ipconfig /all*。</span><span class="sxs-lookup"><span data-stu-id="07593-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="07593-127">此時會顯示您加入的所有 IP 位址，而 DHCP 是關閉的。</span><span class="sxs-lookup"><span data-stu-id="07593-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="07593-128">驗證 (Windows)</span><span class="sxs-lookup"><span data-stu-id="07593-128">Validation (Windows)</span></span>

<span data-ttu-id="07593-129">若要確保您能夠透過相關聯的公用 IP 從第二個 IP 組態連接到網際網路，在使用上述步驟正確地新增該 IP 後，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="07593-129">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, once you have added it correctly using steps above, use the following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="07593-130">對於次要 IP 組態，如果組態有與其相關聯的公用 IP 位址，您只可以 Ping 網際網路。</span><span class="sxs-lookup"><span data-stu-id="07593-130">For secondary IP configurations, you can only ping to the Internet if the configuration has a public IP address associated with it.</span></span> <span data-ttu-id="07593-131">對於主要 IP 組態，公用 IP 位址不需要 Ping 網際網路。</span><span class="sxs-lookup"><span data-stu-id="07593-131">For primary IP configurations, a public IP address is not required to ping to the Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="07593-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="07593-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="07593-133">開啟終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="07593-133">Open a terminal window.</span></span>
2. <span data-ttu-id="07593-134">請確定您是 root 使用者。</span><span class="sxs-lookup"><span data-stu-id="07593-134">Make sure you are the root user.</span></span> <span data-ttu-id="07593-135">如果不是，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="07593-135">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="07593-136">更新網路介面 (假設為 'eth0') 的組態檔。</span><span class="sxs-lookup"><span data-stu-id="07593-136">Update the configuration file of the network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="07593-137">保留針對 dhcp 的現有行。</span><span class="sxs-lookup"><span data-stu-id="07593-137">Keep the existing line item for dhcp.</span></span> <span data-ttu-id="07593-138">主要 IP 位址的設定仍然與先前一樣。</span><span class="sxs-lookup"><span data-stu-id="07593-138">The primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="07593-139">使用下列命令，新增其他靜態 IP 位址的組態︰</span><span class="sxs-lookup"><span data-stu-id="07593-139">Add a configuration for an additional static IP address with the following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="07593-140">您應該會看到一個 .cfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="07593-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="07593-141">開啟 檔案。</span><span class="sxs-lookup"><span data-stu-id="07593-141">Open the file.</span></span> <span data-ttu-id="07593-142">您應該會在檔案結尾看到下列這幾行：</span><span class="sxs-lookup"><span data-stu-id="07593-142">You should see the following lines at the end of the file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="07593-143">在此檔案已有的幾行後面加入下列這幾行︰</span><span class="sxs-lookup"><span data-stu-id="07593-143">Add the following lines after the lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="07593-144">使用下列命令儲存檔案︰</span><span class="sxs-lookup"><span data-stu-id="07593-144">Save the file by using the following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="07593-145">使用下列命令重設網路介面︰</span><span class="sxs-lookup"><span data-stu-id="07593-145">Reset the network interface with the following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="07593-146">如果使用遠端連線，請在同一行中同時執行 ifdown 和 ifup。</span><span class="sxs-lookup"><span data-stu-id="07593-146">Run both ifdown and ifup in the same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="07593-147">使用下列命令確認 IP 位址已加入網路介面︰</span><span class="sxs-lookup"><span data-stu-id="07593-147">Verify the IP address is added to the network interface with the following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="07593-148">您應該會在清單中看到您加入的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="07593-148">You should see the IP address you added as part of the list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="07593-149">Linux (Redhat、CentOS 以及其他)</span><span class="sxs-lookup"><span data-stu-id="07593-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="07593-150">開啟終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="07593-150">Open a terminal window.</span></span>
2. <span data-ttu-id="07593-151">請確定您是 root 使用者。</span><span class="sxs-lookup"><span data-stu-id="07593-151">Make sure you are the root user.</span></span> <span data-ttu-id="07593-152">如果不是，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="07593-152">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="07593-153">輸入您的密碼，並且依照提示的指示。</span><span class="sxs-lookup"><span data-stu-id="07593-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="07593-154">成為 root 使用者之後，使用下列命令瀏覽至網路指令碼資料夾︰</span><span class="sxs-lookup"><span data-stu-id="07593-154">Once you are the root user, navigate to the network scripts folder with the following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="07593-155">使用下列命令列出相關的 ifcfg 檔案︰</span><span class="sxs-lookup"><span data-stu-id="07593-155">List the related ifcfg files using the following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="07593-156">您應該會看到其中一個檔案是 *ifcfg-eth0* 。</span><span class="sxs-lookup"><span data-stu-id="07593-156">You should see *ifcfg-eth0* as one of the files.</span></span>

5. <span data-ttu-id="07593-157">若要新增 IP 位址，如下所示，為其建立組態檔。</span><span class="sxs-lookup"><span data-stu-id="07593-157">To add an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="07593-158">請注意，必須針對每個 IP 組態建立一個檔案。</span><span class="sxs-lookup"><span data-stu-id="07593-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="07593-159">使用下列命令開啟 *ifcfg-eth0:0* 檔案︰</span><span class="sxs-lookup"><span data-stu-id="07593-159">Open the *ifcfg-eth0:0* file with the following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="07593-160">使用下列命令，新增檔案內容，在此案例中為 eth0:0。</span><span class="sxs-lookup"><span data-stu-id="07593-160">Add content to the file, *eth0:0* in this case, with the following command.</span></span> <span data-ttu-id="07593-161">請務必根據您的 IP 位址更新資訊。</span><span class="sxs-lookup"><span data-stu-id="07593-161">Be sure to update information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="07593-162">使用下列命令儲存檔案︰</span><span class="sxs-lookup"><span data-stu-id="07593-162">Save the file with the following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="07593-163">執行下列命令重新啟動網路服務，並確定所做的變更都成功︰</span><span class="sxs-lookup"><span data-stu-id="07593-163">Restart the network services and make sure the changes are successful by running the following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="07593-164">您應該會在傳回的清單中看到您加入的 IP 位址 *eth0:0*。</span><span class="sxs-lookup"><span data-stu-id="07593-164">You should see the IP address you added, *eth0:0*, in the list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="07593-165">驗證 (Linux)</span><span class="sxs-lookup"><span data-stu-id="07593-165">Validation (Linux)</span></span>

<span data-ttu-id="07593-166">若要確保您能夠透過相關聯的公用 IP 從第二個 IP 組態連接到網際網路，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="07593-166">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, use the following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="07593-167">對於次要 IP 組態，如果組態有與其相關聯的公用 IP 位址，您只可以 Ping 網際網路。</span><span class="sxs-lookup"><span data-stu-id="07593-167">For secondary IP configurations, you can only ping to the Internet if the configuration has a public IP address associated with it.</span></span> <span data-ttu-id="07593-168">對於主要 IP 組態，公用 IP 位址不需要 Ping 網際網路。</span><span class="sxs-lookup"><span data-stu-id="07593-168">For primary IP configurations, a public IP address is not required to ping to the Internet.</span></span>

<span data-ttu-id="07593-169">對於 Linux VM，在嘗試驗證來自次要 NIC 的輸出連線能力時，您可能需要新增適當的路由。</span><span class="sxs-lookup"><span data-stu-id="07593-169">For Linux VMs, when trying to validate outbound connectivity from a secondary NIC, you may need to add appropriate routes.</span></span> <span data-ttu-id="07593-170">有許多方法可以執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="07593-170">There are many ways to do this.</span></span> <span data-ttu-id="07593-171">請參閱您的 Linux 散發套件相關文件。</span><span class="sxs-lookup"><span data-stu-id="07593-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="07593-172">以下是完成這項作業的其中一種方法︰</span><span class="sxs-lookup"><span data-stu-id="07593-172">The following is one method to accomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="07593-173">請務必︰</span><span class="sxs-lookup"><span data-stu-id="07593-173">Be sure to replace:</span></span>
    - <span data-ttu-id="07593-174">將 **10.0.0.5** 替換成有相關聯公用 IP 位址的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="07593-174">**10.0.0.5** with the private IP address that has a public IP address associated to it</span></span>
    - <span data-ttu-id="07593-175">將 **10.0.0.1** 替換為您的預設閘道</span><span class="sxs-lookup"><span data-stu-id="07593-175">**10.0.0.1** to your default gateway</span></span>
    - <span data-ttu-id="07593-176">將 **eth2** 替換為您的次要 NIC 名稱</span><span class="sxs-lookup"><span data-stu-id="07593-176">**eth2** to the name of your secondary NIC</span></span>

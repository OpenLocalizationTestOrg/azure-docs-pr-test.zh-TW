## <span data-ttu-id="36206-101"><a name="os-config"></a>新增 IP 位址 tooa VM 作業系統</span><span class="sxs-lookup"><span data-stu-id="36206-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="36206-102">連線並建立具有多個私人 IP 位址的登入 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="36206-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="36206-103">您必須手動加入所有 hello 私人 IP 位址 （包括 hello 主要複本），就像加入 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="36206-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="36206-104">完成下列步驟適用於您的 VM 作業系統的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="36206-105">Windows</span><span class="sxs-lookup"><span data-stu-id="36206-105">Windows</span></span>

1. <span data-ttu-id="36206-106">從命令提示字元輸入 *ipconfig /all*。</span><span class="sxs-lookup"><span data-stu-id="36206-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="36206-107">您只會看見 hello*主要*私人 IP 位址 （透過 DHCP)。</span><span class="sxs-lookup"><span data-stu-id="36206-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="36206-108">型別*ncpa.cpl*在 hello 命令提示字元 tooopen hello**網路連線**視窗。</span><span class="sxs-lookup"><span data-stu-id="36206-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="36206-109">開啟 hello hello 適當的配接器屬性：**區域連線**。</span><span class="sxs-lookup"><span data-stu-id="36206-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="36206-110">按兩下 [網際網路通訊協定第 4 版 (IPv4)]。</span><span class="sxs-lookup"><span data-stu-id="36206-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="36206-111">選取**下列的 IP 位址使用 hello**並輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="36206-112">**IP 位址**： 輸入 hello*主要*私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="36206-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="36206-113">**子網路遮罩**︰根據您的子網路設定。</span><span class="sxs-lookup"><span data-stu-id="36206-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="36206-114">例如，如果 hello 子網路是 / 24 子網路則 hello 子網路遮罩為 255.255.255.0。</span><span class="sxs-lookup"><span data-stu-id="36206-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="36206-115">**預設閘道**: hello hello 子網路中的第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="36206-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="36206-116">如果您的子網路是 10.0.0.0/24，hello 閘道 IP 位址為 10.0.0.1。</span><span class="sxs-lookup"><span data-stu-id="36206-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="36206-117">按一下**下列的 DNS 伺服器位址使用 hello**並輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="36206-118">**慣用 DNS 伺服器**︰如果您不是使用自己的 DNS 伺服器，請輸入 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="36206-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="36206-119">如果您使用您自己的 DNS 伺服器，輸入您的伺服器 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="36206-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="36206-120">按一下 hello**進階**按鈕，然後加入其他 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="36206-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="36206-121">新增的每個 hello 次要私用 IP 位址列入的 hello hello 主要 IP 位址的指定相同的子網路的步驟 8 toohello NIC。</span><span class="sxs-lookup"><span data-stu-id="36206-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="36206-122">如果未正確地依照 hello 上述步驟，您可能會失去連線 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="36206-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="36206-123">請確定輸入的步驟 5 的 hello 資訊正確無誤後再繼續。</span><span class="sxs-lookup"><span data-stu-id="36206-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="36206-124">按一下**[確定]** tooclose 出 hello TCP/IP 設定，然後**確定**再次 tooclose hello 介面卡的設定。</span><span class="sxs-lookup"><span data-stu-id="36206-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="36206-125">您的 RDP 連接已重建。</span><span class="sxs-lookup"><span data-stu-id="36206-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="36206-126">從命令提示字元輸入 *ipconfig /all*。</span><span class="sxs-lookup"><span data-stu-id="36206-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="36206-127">此時會顯示您加入的所有 IP 位址，而 DHCP 是關閉的。</span><span class="sxs-lookup"><span data-stu-id="36206-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="36206-128">驗證 (Windows)</span><span class="sxs-lookup"><span data-stu-id="36206-128">Validation (Windows)</span></span>

<span data-ttu-id="36206-129">tooensure 都能 tooconnect toohello 上面步驟從透過公用 IP 相關聯，一旦您加入它使用正確的 hello 次要 IP 設定的網際網路，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="36206-130">對於次要 IP 設定，您只可以 ping toohello 網際網路如果 hello 組態都有與其相關聯的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="36206-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="36206-131">主要的 IP 組態的公用 IP 位址不需要的 tooping toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="36206-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="36206-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="36206-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="36206-133">開啟終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="36206-133">Open a terminal window.</span></span>
2. <span data-ttu-id="36206-134">請確定您是 hello 根使用者。</span><span class="sxs-lookup"><span data-stu-id="36206-134">Make sure you are hello root user.</span></span> <span data-ttu-id="36206-135">如果您不是，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="36206-136">更新 hello hello （假設 'eth0'） 的網路介面的組態檔。</span><span class="sxs-lookup"><span data-stu-id="36206-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="36206-137">保留 hello 現有明細項目 dhcp。</span><span class="sxs-lookup"><span data-stu-id="36206-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="36206-138">在先前 hello 主要 IP 位址依然會設定。</span><span class="sxs-lookup"><span data-stu-id="36206-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="36206-139">加入額外的靜態 IP 位址組態，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="36206-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="36206-140">您應該會看到一個 .cfg 檔案。</span><span class="sxs-lookup"><span data-stu-id="36206-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="36206-141">開啟 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="36206-141">Open hello file.</span></span> <span data-ttu-id="36206-142">您應該會看到下列行 hello hello 檔結尾的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="36206-143">加入下列行之後存在此檔案中的 hello 行 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="36206-144">使用下列命令的 hello 儲存 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="36206-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="36206-145">重設 hello 網路介面，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="36206-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="36206-146">請執行 ifdown 和 ifup 中相同列如果使用遠端連線的 hello。</span><span class="sxs-lookup"><span data-stu-id="36206-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="36206-147">請確認 hello IP 位址加入 toohello 網路介面以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="36206-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="36206-148">您應該會看到 hello IP 位址您加入 hello 清單的一部分。</span><span class="sxs-lookup"><span data-stu-id="36206-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="36206-149">Linux (Redhat、CentOS 以及其他)</span><span class="sxs-lookup"><span data-stu-id="36206-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="36206-150">開啟終端機視窗。</span><span class="sxs-lookup"><span data-stu-id="36206-150">Open a terminal window.</span></span>
2. <span data-ttu-id="36206-151">請確定您是 hello 根使用者。</span><span class="sxs-lookup"><span data-stu-id="36206-151">Make sure you are hello root user.</span></span> <span data-ttu-id="36206-152">如果您不是，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="36206-153">輸入您的密碼，並且依照提示的指示。</span><span class="sxs-lookup"><span data-stu-id="36206-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="36206-154">一旦 hello 根使用者，請瀏覽 toohello 網路指令碼 資料夾，以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="36206-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="36206-155">清單 hello 相關 ifcfg 檔案使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="36206-156">您應該會看到*ifcfg eth0*做為其中一個 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="36206-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="36206-157">tooadd IP 位址，為其建立組態檔，如下所示。</span><span class="sxs-lookup"><span data-stu-id="36206-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="36206-158">請注意，必須針對每個 IP 組態建立一個檔案。</span><span class="sxs-lookup"><span data-stu-id="36206-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="36206-159">開啟 hello *ifcfg-eth0:0*檔案以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="36206-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="36206-160">加入內容 toohello 檔案*eth0:0*在此情況下，使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="36206-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="36206-161">確定 tooupdate 資訊可根據您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="36206-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="36206-162">儲存 hello 檔案以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="36206-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="36206-163">重新啟動 hello 網路服務，並確定 hello 變更都能藉由執行下列命令的 hello 成功：</span><span class="sxs-lookup"><span data-stu-id="36206-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="36206-164">您應該會看見 hello IP 位址加入，您*eth0:0*，傳回的 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="36206-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="36206-165">驗證 (Linux)</span><span class="sxs-lookup"><span data-stu-id="36206-165">Validation (Linux)</span></span>

<span data-ttu-id="36206-166">從次要 IP 設定 hello 公用 IP 透過網際網路相關它都能夠 tooconnect toohello tooensure，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="36206-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="36206-167">對於次要 IP 設定，您只可以 ping toohello 網際網路如果 hello 組態都有與其相關聯的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="36206-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="36206-168">主要的 IP 組態的公用 IP 位址不需要的 tooping toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="36206-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="36206-169">適用於 Linux Vm，嘗試從次要 NIC toovalidate 輸出連線時，您可能需要 tooadd 適當的路由。</span><span class="sxs-lookup"><span data-stu-id="36206-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="36206-170">有許多方式 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="36206-170">There are many ways toodo this.</span></span> <span data-ttu-id="36206-171">請參閱您的 Linux 散發套件相關文件。</span><span class="sxs-lookup"><span data-stu-id="36206-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="36206-172">hello 下列這是一個方法 tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="36206-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="36206-173">為確定 tooreplace:</span><span class="sxs-lookup"><span data-stu-id="36206-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="36206-174">**10.0.0.5**具有 hello 私人 IP 位址具有公用 IP 位址相關聯的 tooit</span><span class="sxs-lookup"><span data-stu-id="36206-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="36206-175">**10.0.0.1** tooyour 預設閘道</span><span class="sxs-lookup"><span data-stu-id="36206-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="36206-176">**eth2**您次要 NIC toohello 名稱</span><span class="sxs-lookup"><span data-stu-id="36206-176">**eth2** toohello name of your secondary NIC</span></span>

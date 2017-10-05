---
title: "在 Azure 中使用遠端桌面連接至 Linux VM | Microsoft Docs"
description: "了解如何安裝和設定遠端桌面 (xrdp)，以使用圖形化工具在 Azure 中連接至 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="28df4-103">在 Azure 中安裝和設定遠端桌面，以連接至 Linux VM</span><span class="sxs-lookup"><span data-stu-id="28df4-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="28df4-104">在 Azure 中的 Linux 虛擬機器 (VM) 通常是使用安全殼層 (SSH) 連接從命令列管理。</span><span class="sxs-lookup"><span data-stu-id="28df4-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="28df4-105">如果是 Linux 的新手，或者是快速疑難排解的案例，使用遠端桌面可能會比較容易。</span><span class="sxs-lookup"><span data-stu-id="28df4-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="28df4-106">本文將詳細說明如何使用 Resource Manager 部署模型為您的 Linux VM 安裝和設定桌面環境 ([xfce](https://www.xfce.org)) 和遠端桌面 ([xrdp](http://www.xrdp.org))。</span><span class="sxs-lookup"><span data-stu-id="28df4-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="28df4-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="28df4-107">Prerequisites</span></span>
<span data-ttu-id="28df4-108">這篇文章需要在 Azure 中有現有的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="28df4-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="28df4-109">如果您需要建立 VM，請使用下列其中一個方法︰</span><span class="sxs-lookup"><span data-stu-id="28df4-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="28df4-110">[Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="28df4-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="28df4-111">[Azure 入口網站](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="28df4-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="28df4-112">在 Linux VM 上安裝桌面環境</span><span class="sxs-lookup"><span data-stu-id="28df4-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="28df4-113">在 Azure 中大多數 Linux VM 預設沒有安裝桌面環境。</span><span class="sxs-lookup"><span data-stu-id="28df4-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="28df4-114">Linux VM 通常是使用 SSH 連接來管理，而不是使用桌面環境來管理。</span><span class="sxs-lookup"><span data-stu-id="28df4-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="28df4-115">在 Linux 中您有各種不同的桌面環境可以選擇。</span><span class="sxs-lookup"><span data-stu-id="28df4-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="28df4-116">根據您選擇的桌面環境，可能會使用 1 到 2 GB 的磁碟空間，並且需要 5 到 10 分鐘，才能安裝及設定所有必要的套件。</span><span class="sxs-lookup"><span data-stu-id="28df4-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="28df4-117">下列範例會在 Ubuntu VM 上安裝輕量型 [xfce4](https://www.xfce.org/) 桌面環境。</span><span class="sxs-lookup"><span data-stu-id="28df4-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="28df4-118">其他散發的命令稍微不同 (例如，使用 `yum` 以在 Red Hat Enterprise Linux 上安裝及設定適當的 `selinux` 規則，或使用 `zypper` 在 SUSE 上安裝)。</span><span class="sxs-lookup"><span data-stu-id="28df4-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="28df4-119">首先，SSH 連接至您的 VM。</span><span class="sxs-lookup"><span data-stu-id="28df4-119">First, SSH to your VM.</span></span> <span data-ttu-id="28df4-120">下列範例會連線至名為 myvm.westus.cloudapp.azure.com 且具有使用者名稱 azureuser 的 VM：</span><span class="sxs-lookup"><span data-stu-id="28df4-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="28df4-121">如果您使用 Windows，並且需要使用 SSH 的詳細資訊，請參閱[如何使用 SSH 金鑰與 Windows](ssh-from-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="28df4-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="28df4-122">接下來，使用 `apt` 安裝 xfce，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28df4-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="28df4-123">安裝及設定遠端桌面伺服器</span><span class="sxs-lookup"><span data-stu-id="28df4-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="28df4-124">現在您已安裝桌面環境，設定遠端桌面服務來接聽連入連線。</span><span class="sxs-lookup"><span data-stu-id="28df4-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="28df4-125">[xrdp](http://xrdp.org) 是開放原始碼遠端桌面通訊協定 (RDP) 伺服器，適用於大部分的 Linux 散發套件，而且很適合處理 xfce。</span><span class="sxs-lookup"><span data-stu-id="28df4-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="28df4-126">在您的 Ubuntu VM 上安裝 xrdp，如下所示：</span><span class="sxs-lookup"><span data-stu-id="28df4-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="28df4-127">告訴 xrdp 當您啟動工作階段時要使用的桌面環境。</span><span class="sxs-lookup"><span data-stu-id="28df4-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="28df4-128">設定 xrdp 以使用 xfce 做為您的桌面環境，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28df4-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="28df4-129">重新啟動 xrdp 服務，讓變更生效，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28df4-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="28df4-130">設定本機使用者帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="28df4-130">Set a local user account password</span></span>
<span data-ttu-id="28df4-131">如果您在建立 VM 時已為您的使用者帳戶建立密碼，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="28df4-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="28df4-132">如果您只使用 SSH 金鑰驗證，並且尚未設定本機帳戶密碼，請先指定密碼，再使用 xrdp 登入您的 VM。</span><span class="sxs-lookup"><span data-stu-id="28df4-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="28df4-133">xrdp 無法接受 SSH 金鑰進行驗證。</span><span class="sxs-lookup"><span data-stu-id="28df4-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="28df4-134">下列範例會指定使用者帳戶 azureuser 的密碼：</span><span class="sxs-lookup"><span data-stu-id="28df4-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="28df4-135">如果目前不允許密碼登入，則指定密碼不會將 SSHD 組態更新為允許密碼登入。</span><span class="sxs-lookup"><span data-stu-id="28df4-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="28df4-136">從安全性的觀點而言，您可能想要使用金鑰型驗證的 SSH 通道連接至 VM，然後連接到 xrdp。</span><span class="sxs-lookup"><span data-stu-id="28df4-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="28df4-137">如果是這樣，請略過下一個步驟 (建立網路安全性群組規則) 以允許遠端桌面流量。</span><span class="sxs-lookup"><span data-stu-id="28df4-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="28df4-138">建立遠端桌面流量的網路安全性群組規則</span><span class="sxs-lookup"><span data-stu-id="28df4-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="28df4-139">若要允許遠端桌面流量觸達您的 Linux VM，必須建立網路安全性群組規則，允許連接埠 3389 上的 TCP 觸達您的 VM。</span><span class="sxs-lookup"><span data-stu-id="28df4-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="28df4-140">如需有關網路安全性群組規則的詳細資訊，請參閱[什麼是網路安全性群組？](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28df4-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="28df4-141">您也可以[使用 Azure 入口網站建立網路安全性群組規則](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="28df4-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="28df4-142">下列範例使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 建立名為 myNetworkSecurityGroupRule 的網路安全性群組規則，以「允許」 tcp 連接埠 *3389* 的流量。</span><span class="sxs-lookup"><span data-stu-id="28df4-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="28df4-143">連接 Linux VM 與遠端桌面用戶端</span><span class="sxs-lookup"><span data-stu-id="28df4-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="28df4-144">開啟您的本機遠端桌面用戶端，並連接至 Linux VM 的 IP 位址或 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="28df4-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="28df4-145">在您的 VM 上輸入使用者帳戶的使用者名稱和密碼，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28df4-145">Enter the username and password for the user account on your VM as follows:</span></span>

![使用遠端桌面用戶端連接至 xrdp](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="28df4-147">驗證之後，會載入 xfce 桌面環境，看起來類似下列範例︰</span><span class="sxs-lookup"><span data-stu-id="28df4-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![透過 xrdp 的 xfce 桌面環境](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="28df4-149">疑難排解</span><span class="sxs-lookup"><span data-stu-id="28df4-149">Troubleshoot</span></span>
<span data-ttu-id="28df4-150">如果無法使用遠端桌面用戶端連接至 Linux VM，請在 Linux VM 上使用 `netstat`，以檢查您的 VM 是否正在接聽 RDP 連線，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28df4-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="28df4-151">下列範例顯示 VM 如預期地接聽 TCP 連接埠 3389：</span><span class="sxs-lookup"><span data-stu-id="28df4-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="28df4-152">如果未接聽 xrdp 服務，在 Ubuntu VM 上重新啟動服務，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="28df4-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="28df4-153">在您的 Ubuntu VM 上檢閱 /var/logThug 中的記錄，以取得為何服務沒有回應的指示。</span><span class="sxs-lookup"><span data-stu-id="28df4-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="28df4-154">您也可以在遠端桌面連線嘗試期間監視 syslog，以檢視任何錯誤：</span><span class="sxs-lookup"><span data-stu-id="28df4-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="28df4-155">Red Hat Enterprise Linux 和 SUSE 等其他 Linux 散發重新啟動服務的方式可能有所不同，要檢閱的記錄檔位置也不同。</span><span class="sxs-lookup"><span data-stu-id="28df4-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="28df4-156">如果您未在遠端桌面用戶端收到任何回應，而且在系統記錄檔中看不到任何事件，這種行為表示遠端桌面流量無法觸達 VM。</span><span class="sxs-lookup"><span data-stu-id="28df4-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="28df4-157">檢閱網路安全性群組規則，以確保您擁有規則以允許連接埠 3389 上的 TCP。</span><span class="sxs-lookup"><span data-stu-id="28df4-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="28df4-158">如需詳細資訊，請參閱[針對應用程式連線能力問題進行疑難排解](../windows/troubleshoot-app-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="28df4-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="28df4-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28df4-159">Next steps</span></span>
<span data-ttu-id="28df4-160">如需有關建立和使用 SSH 金鑰與 Linux VM 的詳細資訊，請參閱[在 Azure 中為 Linux VM 建立 SSH 金鑰](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="28df4-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="28df4-161">如需從 Windows 使用 SSH 的詳細資訊，請參閱[如何以 Windows 使用 SSH 金鑰](ssh-from-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="28df4-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>


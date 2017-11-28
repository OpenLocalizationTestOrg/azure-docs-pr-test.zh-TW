---
title: "aaaUse 在 Azure 中的 Linux VM 的遠端桌面 tooa |Microsoft 文件"
description: "深入了解如何 tooinstall 並在 Azure 中使用圖形化工具中設定遠端桌面 (xrdp) tooconnect tooa Linux VM"
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
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="4787d-103">安裝並在 Azure 中設定遠端桌面 tooconnect tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="4787d-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="4787d-104">在 Azure 中 Linux 虛擬機器 (Vm) 通常是使用安全殼層 (SSH) 連線的 hello 命令列管理。</span><span class="sxs-lookup"><span data-stu-id="4787d-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="4787d-105">當新的 tooLinux 或快速疑難排解案例中，遠端桌面的 hello 使用可能會比較容易。</span><span class="sxs-lookup"><span data-stu-id="4787d-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="4787d-106">此發行項詳細資料時，如何 tooinstall 及設定使用的桌面環境 ([xfce](https://www.xfce.org)) 和遠端桌面 ([xrdp](http://www.xrdp.org)) Linux vm 使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4787d-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4787d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4787d-107">Prerequisites</span></span>
<span data-ttu-id="4787d-108">這篇文章需要在 Azure 中有現有的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="4787d-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="4787d-109">如果您需要 toocreate VM，使用下列方法 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="4787d-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="4787d-110">hello [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="4787d-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="4787d-111">hello [Azure 入口網站](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4787d-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="4787d-112">在 Linux VM 上安裝桌面環境</span><span class="sxs-lookup"><span data-stu-id="4787d-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="4787d-113">在 Azure 中大多數 Linux VM 預設沒有安裝桌面環境。</span><span class="sxs-lookup"><span data-stu-id="4787d-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="4787d-114">Linux VM 通常是使用 SSH 連接來管理，而不是使用桌面環境來管理。</span><span class="sxs-lookup"><span data-stu-id="4787d-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="4787d-115">在 Linux 中您有各種不同的桌面環境可以選擇。</span><span class="sxs-lookup"><span data-stu-id="4787d-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="4787d-116">根據您選擇的桌面環境中，它可能會取用一個 too2 GB 的磁碟空間，並採取 5 too10 分鐘 tooinstall 和設定所有必要的 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="4787d-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="4787d-117">hello 以下範例會安裝 hello 輕量型[xfce4](https://www.xfce.org/) Ubuntu 虛擬機器上的桌面環境。</span><span class="sxs-lookup"><span data-stu-id="4787d-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="4787d-118">針對其他分佈會稍微不同的命令 (使用`yum`tooinstall Red Hat Enterprise Linux 上的並設定適當`selinux`規則或使用`zypper`tooinstall 上 SUSE，例如)。</span><span class="sxs-lookup"><span data-stu-id="4787d-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="4787d-119">首先，SSH tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="4787d-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="4787d-120">hello 下列範例會連接 toohello 名為 VM *myvm.westus.cloudapp.azure.com*的 hello username *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="4787d-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="4787d-121">如果您使用 Windows，且需要有關使用 SSH 詳細資訊，請參閱[toouse SSH 與 Windows 的索引鍵](ssh-from-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="4787d-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="4787d-122">接下來，使用 `apt` 安裝 xfce，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4787d-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="4787d-123">安裝及設定遠端桌面伺服器</span><span class="sxs-lookup"><span data-stu-id="4787d-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="4787d-124">既然您已安裝的桌面環境時，設定連入連線的遠端桌面服務 toolisten。</span><span class="sxs-lookup"><span data-stu-id="4787d-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="4787d-125">[xrdp](http://xrdp.org) 是開放原始碼遠端桌面通訊協定 (RDP) 伺服器，適用於大部分的 Linux 散發套件，而且很適合處理 xfce。</span><span class="sxs-lookup"><span data-stu-id="4787d-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="4787d-126">在您的 Ubuntu VM 上安裝 xrdp，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4787d-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="4787d-127">當您啟動您的工作階段時告訴 xrdp 哪些桌面環境 toouse。</span><span class="sxs-lookup"><span data-stu-id="4787d-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="4787d-128">設定 xrdp toouse xfce 做為您的桌面環境，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4787d-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="4787d-129">重新啟動 hello 變更 tootake 效果 hello xrdp 服務如下：</span><span class="sxs-lookup"><span data-stu-id="4787d-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="4787d-130">設定本機使用者帳戶密碼</span><span class="sxs-lookup"><span data-stu-id="4787d-130">Set a local user account password</span></span>
<span data-ttu-id="4787d-131">如果您在建立 VM 時已為您的使用者帳戶建立密碼，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="4787d-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="4787d-132">如果您只使用 SSH 金鑰驗證，並不需要設定，指定密碼，才能使用 xrdp toolog tooyour VM 中的本機帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="4787d-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="4787d-133">xrdp 無法接受 SSH 金鑰進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4787d-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="4787d-134">hello 下列範例會指定 hello 使用者帳戶的密碼*azureuser*:</span><span class="sxs-lookup"><span data-stu-id="4787d-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="4787d-135">如果它目前並不會並指定密碼並不會更新您 SSHD 組態 toopermit 密碼登入。</span><span class="sxs-lookup"><span data-stu-id="4787d-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="4787d-136">從安全性觀點來看，您可能想 tooconnect tooyour VM 使用 SSH 通道使用索引鍵為基礎的驗證，並再連接 tooxrdp。</span><span class="sxs-lookup"><span data-stu-id="4787d-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="4787d-137">若是如此，請略過下列步驟建立網路安全性群組規則 tooallow 遠端桌面流量 hello。</span><span class="sxs-lookup"><span data-stu-id="4787d-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="4787d-138">建立遠端桌面流量的網路安全性群組規則</span><span class="sxs-lookup"><span data-stu-id="4787d-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="4787d-139">tooallow 遠端桌面流量 tooreach Linux VM，網路安全性群組規則需要建立 toobe，允許 TCP 連接埠 3389 tooreach 上的 VM。</span><span class="sxs-lookup"><span data-stu-id="4787d-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="4787d-140">如需有關網路安全性群組規則的詳細資訊，請參閱[什麼是網路安全性群組？](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4787d-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="4787d-141">您也可以[使用 hello Azure 入口網站 toocreate 網路安全性群組規則](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4787d-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4787d-142">hello 下列範例會建立網路安全性群組規則與[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)名為*myNetworkSecurityGroupRule*太*允許*上的流量*tcp*連接埠*3389*。</span><span class="sxs-lookup"><span data-stu-id="4787d-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="4787d-143">連接 Linux VM 與遠端桌面用戶端</span><span class="sxs-lookup"><span data-stu-id="4787d-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="4787d-144">開啟您本機的遠端桌面用戶端，並連接 toohello IP 位址或 Linux VM 的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4787d-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="4787d-145">Hello 使用者名稱和密碼 hello 使用者帳戶上輸入您的 VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4787d-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![連接 tooxrdp 使用您的遠端桌面用戶端](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="4787d-147">驗證之後，將會載入 hello xfce 桌面環境，並將其看起來類似下列範例的 toohello 中：</span><span class="sxs-lookup"><span data-stu-id="4787d-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![透過 xrdp 的 xfce 桌面環境](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="4787d-149">疑難排解</span><span class="sxs-lookup"><span data-stu-id="4787d-149">Troubleshoot</span></span>
<span data-ttu-id="4787d-150">如果您無法連接 tooyour 使用遠端桌面用戶端的 Linux VM，使用`netstat`您 Linux VM tooverify，如下所示接聽 RDP 連線您的 VM 上：</span><span class="sxs-lookup"><span data-stu-id="4787d-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="4787d-151">下列範例所示的 hello hello 接聽 TCP 連接埠 3389，如預期般的 VM:</span><span class="sxs-lookup"><span data-stu-id="4787d-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="4787d-152">如果 hello xrdp 服務沒有在接聽，Ubuntu 虛擬機器上重新啟動 hello 服務，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4787d-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="4787d-153">檢閱記錄檔*/var/記錄*群惡棍為 toowhy hello 服務的指示 Ubuntu VM 上可能沒有回應。</span><span class="sxs-lookup"><span data-stu-id="4787d-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="4787d-154">您也可以監視 hello syslog 遠端桌面連線嘗試 tooview 期間的任何錯誤：</span><span class="sxs-lookup"><span data-stu-id="4787d-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="4787d-155">其他 Linux 散發套件，例如 Red Hat Enterprise Linux 和 SUSE 可能會有不同的方式 toorestart 服務和其他記錄檔位置 tooreview。</span><span class="sxs-lookup"><span data-stu-id="4787d-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="4787d-156">如果您不在您的遠端桌面用戶端會收到任何回應，並不會看到 hello 系統記錄檔中的任何事件，這種行為表示遠端桌面流量無法連線到 hello VM。</span><span class="sxs-lookup"><span data-stu-id="4787d-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="4787d-157">檢閱您所規則 toopermit TCP 連接埠 3389 上您網路安全性群組規則 tooensure。</span><span class="sxs-lookup"><span data-stu-id="4787d-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="4787d-158">如需詳細資訊，請參閱[針對應用程式連線能力問題進行疑難排解](../windows/troubleshoot-app-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="4787d-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4787d-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4787d-159">Next steps</span></span>
<span data-ttu-id="4787d-160">如需有關建立和使用 SSH 金鑰與 Linux VM 的詳細資訊，請參閱[在 Azure 中為 Linux VM 建立 SSH 金鑰](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="4787d-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="4787d-161">如需從 Windows 使用 SSH 資訊，請參閱[toouse SSH 與 Windows 的索引鍵](ssh-from-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="4787d-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>


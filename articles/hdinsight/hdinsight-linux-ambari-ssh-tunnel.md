---
title: "使用 SSH 通道存取 Azure HDInsight | Microsoft Docs"
description: "了解如何使用 SSH 通道，安全地瀏覽以 Linux 為基礎的 HDInsight 節點上裝載的 Web 資源。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="6dccb-103">使用 SSH 通道來存取 Ambari Web UI、JobHistory、NameNode、Oozie 及其他 Web UI</span><span class="sxs-lookup"><span data-stu-id="6dccb-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="6dccb-104">以 Linux 為基礎的 HDInsight 叢集可讓您透過網際網路存取 Ambari Web UI，但無法存取 UI 的某些功能。</span><span class="sxs-lookup"><span data-stu-id="6dccb-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="6dccb-105">例如，經由 Ambari 呈現的其他服務的 Web UI。</span><span class="sxs-lookup"><span data-stu-id="6dccb-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="6dccb-106">若要使用 Ambari Web UI 的完整功能，您必須在叢集前端使用 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="6dccb-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="6dccb-107">為何要使用 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="6dccb-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="6dccb-108">Ambari 中的數個功能表只有透過 SSH 通道才能運作。</span><span class="sxs-lookup"><span data-stu-id="6dccb-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="6dccb-109">這些功能表依賴其他節點類型上執行的網站和服務，例如背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="6dccb-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="6dccb-110">通常這些網站並未受到保護，因此直接在網際網路上公開並不安全。</span><span class="sxs-lookup"><span data-stu-id="6dccb-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="6dccb-111">下列 Web UI 需要 SSH 通道：</span><span class="sxs-lookup"><span data-stu-id="6dccb-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="6dccb-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="6dccb-112">JobHistory</span></span>
* <span data-ttu-id="6dccb-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="6dccb-113">NameNode</span></span>
* <span data-ttu-id="6dccb-114">執行緒堆疊</span><span class="sxs-lookup"><span data-stu-id="6dccb-114">Thread Stacks</span></span>
* <span data-ttu-id="6dccb-115">Oozie Web UI</span><span class="sxs-lookup"><span data-stu-id="6dccb-115">Oozie web UI</span></span>
* <span data-ttu-id="6dccb-116">HBase Master 和記錄 UI</span><span class="sxs-lookup"><span data-stu-id="6dccb-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="6dccb-117">如果您使用指令碼動作來自訂叢集，則您安裝的任何服務或公用程式，都會需要 SSH 通道才能公開 Web UI。</span><span class="sxs-lookup"><span data-stu-id="6dccb-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="6dccb-118">例如，如果您使用指令碼動作安裝 Hue，就必須使用 SSH 通道來存取 Hue Web UI。</span><span class="sxs-lookup"><span data-stu-id="6dccb-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dccb-119">如果您透過虛擬網路直接存取 HDInsight，便不需要使用 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="6dccb-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="6dccb-120">如需透過虛擬網路直接存取 HDInsight 的範例，請參閱[將 HDInsight 連線至內部部署網](connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6dccb-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="6dccb-121">什麼是 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="6dccb-121">What is an SSH tunnel</span></span>

<span data-ttu-id="6dccb-122">[安全殼層 (SSH) 通道](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling)會路由傳送傳送至本機工作站上連接埠的流量。</span><span class="sxs-lookup"><span data-stu-id="6dccb-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="6dccb-123">流量是透過與 HDInsight 叢集前端節點的 SSH 連線進行路由傳送。</span><span class="sxs-lookup"><span data-stu-id="6dccb-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="6dccb-124">解析要求的方式就像它是源自前端節點一樣。</span><span class="sxs-lookup"><span data-stu-id="6dccb-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="6dccb-125">接著，透過工作站的通道，將回應路由傳送回去。</span><span class="sxs-lookup"><span data-stu-id="6dccb-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6dccb-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="6dccb-126">Prerequisites</span></span>

* <span data-ttu-id="6dccb-127">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6dccb-127">An SSH client.</span></span> <span data-ttu-id="6dccb-128">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="6dccb-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="6dccb-129">可以設定為使用 SOCKS5 Proxy 的網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6dccb-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="6dccb-130">Windows 的內建 SOCKS Proxy 支援不支援 SOCKS5，並且不適用此文件中的步驟。</span><span class="sxs-lookup"><span data-stu-id="6dccb-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="6dccb-131">下列瀏覽器會仰賴 Windows Proxy 設定，而且目前不適用本文件中的步驟︰</span><span class="sxs-lookup"><span data-stu-id="6dccb-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="6dccb-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="6dccb-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="6dccb-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="6dccb-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="6dccb-134">Google Chrome 也會依賴 Windows Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="6dccb-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="6dccb-135">不過，您可以安裝支援 SOCKS5 的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="6dccb-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="6dccb-136">我們建議使用 [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)。</span><span class="sxs-lookup"><span data-stu-id="6dccb-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="6dccb-137"><a name="usessh"></a>使用 SSH 命令建立通道</span><span class="sxs-lookup"><span data-stu-id="6dccb-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="6dccb-138">使用下列命令，利用 `ssh` 命令建立 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="6dccb-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="6dccb-139">以您 HDInsight 叢集的 SSH 使用者取代 **USERNAME**，並以您 HDInsight 叢集的名稱取代 **CLUSTERNAME**：</span><span class="sxs-lookup"><span data-stu-id="6dccb-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="6dccb-140">此命令會建立透過 SSH 將流量由本機連接埠 9876 路由傳送至叢集的連線。</span><span class="sxs-lookup"><span data-stu-id="6dccb-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="6dccb-141">可用選項包括：</span><span class="sxs-lookup"><span data-stu-id="6dccb-141">The options are:</span></span>

* <span data-ttu-id="6dccb-142">**D 9876** - 會透過通道路由傳送流量的本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dccb-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="6dccb-143">**C** - 壓縮所有資料，因為網路流量大多是文字。</span><span class="sxs-lookup"><span data-stu-id="6dccb-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="6dccb-144">**2** - 強制 SSH 僅嘗試通訊協定第 2 版。</span><span class="sxs-lookup"><span data-stu-id="6dccb-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="6dccb-145">**q** - 無訊息模式。</span><span class="sxs-lookup"><span data-stu-id="6dccb-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="6dccb-146">**T** - 停用虛擬 tty 配置，因為我們只是轉送連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dccb-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6dccb-147">**n** - 防止讀取 STDIN，因為我們只是轉送連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dccb-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6dccb-148">**N** - 不執行遠端命令，因為我們只是轉送連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dccb-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="6dccb-149">**f** - 在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="6dccb-149">**f** - Run in the background.</span></span>

<span data-ttu-id="6dccb-150">在命令完成後，會將傳送至本機電腦上連接埠 9876 的流量路由傳送至叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="6dccb-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="6dccb-151"><a name="useputty"></a>使用 PuTTY 建立通道</span><span class="sxs-lookup"><span data-stu-id="6dccb-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="6dccb-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) 是適用於 Windows 的圖形化 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="6dccb-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="6dccb-153">使用下列步驟，利用 PuTTY 建立 SSH 通道：</span><span class="sxs-lookup"><span data-stu-id="6dccb-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="6dccb-154">開啟 PuTTY，並輸入連線資訊。</span><span class="sxs-lookup"><span data-stu-id="6dccb-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="6dccb-155">如果您不熟悉 PuTTY，請參閱 [PuTTY 文件 (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html) (英文)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)。</span><span class="sxs-lookup"><span data-stu-id="6dccb-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="6dccb-156">在對話方塊左側的 [類別] 區段中，依序展開 [連接] 和 [SSH]，最後選取 [通道]。</span><span class="sxs-lookup"><span data-stu-id="6dccb-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="6dccb-157">在 [ **控制 SSH 連接埠轉送的選項** ] 表單中提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="6dccb-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="6dccb-158">**來源連接埠** - 您想要轉送之用戶端上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="6dccb-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="6dccb-159">例如， **9876**。</span><span class="sxs-lookup"><span data-stu-id="6dccb-159">For example, **9876**.</span></span>

   * <span data-ttu-id="6dccb-160">**目的地** - 以 Linux 為基礎的 HDInsight 叢集的 SSH 位址。</span><span class="sxs-lookup"><span data-stu-id="6dccb-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6dccb-161">例如， **mycluster-ssh.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="6dccb-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="6dccb-162">**動態** - 啟用動態 SOCKS Proxy 路由。</span><span class="sxs-lookup"><span data-stu-id="6dccb-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![通道處理選項的影像](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="6dccb-164">按一下 [新增] 以新增設定，然後按一下 [開啟] 開啟 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="6dccb-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="6dccb-165">出現提示時，登入伺服器。</span><span class="sxs-lookup"><span data-stu-id="6dccb-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="6dccb-166">從瀏覽器使用通道</span><span class="sxs-lookup"><span data-stu-id="6dccb-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dccb-167">本節中的步驟使用 Mozilla FireFox 瀏覽器，因為它在所有平台上提供相同的 Proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="6dccb-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="6dccb-168">其他現代瀏覽器 (例如 Google Chrome) 可能需要延伸模組 (例如 FoxyProxy) 才能使用通道。</span><span class="sxs-lookup"><span data-stu-id="6dccb-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="6dccb-169">將瀏覽器設定為使用建立通道時所使用的 **localhost** 和連接埠做為 **SOCKS v5** Proxy。</span><span class="sxs-lookup"><span data-stu-id="6dccb-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="6dccb-170">Firefox 的設定如下所示。</span><span class="sxs-lookup"><span data-stu-id="6dccb-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="6dccb-171">如果您使用與 9876 不同的連接埠，請將連接埠變更為您所用的連接埠：</span><span class="sxs-lookup"><span data-stu-id="6dccb-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![Firefox 設定的影像](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="6dccb-173">選取 [遠端 DNS] 會使用 HDInsight 叢集解析網域名稱系統 (DNS) 要求。</span><span class="sxs-lookup"><span data-stu-id="6dccb-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="6dccb-174">這項設定會使用叢集的前端節點來解析 DNS。</span><span class="sxs-lookup"><span data-stu-id="6dccb-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="6dccb-175">請瀏覽 [http://www.whatismyip.com/](http://www.whatismyip.com/) 這類網站，驗證通道可以運作。</span><span class="sxs-lookup"><span data-stu-id="6dccb-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="6dccb-176">傳回的 IP 應該是 Microsoft Azure 資料中心使用的 IP。</span><span class="sxs-lookup"><span data-stu-id="6dccb-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="6dccb-177">驗證 Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="6dccb-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="6dccb-178">建立叢集後，請使用下列步驟來確認您可以從 Ambari Web 存取服務 Web UI：</span><span class="sxs-lookup"><span data-stu-id="6dccb-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="6dccb-179">在瀏覽器中，移至 http://headnodehost:8080 。</span><span class="sxs-lookup"><span data-stu-id="6dccb-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="6dccb-180">`headnodehost` 位址會透過通道傳送到叢集，並解析為執行 Ambari 的前端節點。</span><span class="sxs-lookup"><span data-stu-id="6dccb-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="6dccb-181">出現提示時，請輸入您叢集的管理員使用者名稱 (admin) 和密碼。</span><span class="sxs-lookup"><span data-stu-id="6dccb-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="6dccb-182">Ambari Web UI 可能會出現第二次的提示。</span><span class="sxs-lookup"><span data-stu-id="6dccb-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="6dccb-183">若是如此，請重新輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="6dccb-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6dccb-184">使用 http://headnodehost:8080 位址連線至叢集時，表示您是透過通道進行連線。</span><span class="sxs-lookup"><span data-stu-id="6dccb-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="6dccb-185">通訊是使用 SSH 通道進行保護，而非 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="6dccb-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="6dccb-186">若要透過 HTTPS 與網際網路連接，請使用 https://CLUSTERNAME.azurehdinsight.net，其中 **CLUSTERNAME** 是叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="6dccb-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="6dccb-187">在 Ambari Web UI 中，選取頁面左邊清單中的 HDFS。</span><span class="sxs-lookup"><span data-stu-id="6dccb-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![選取 HDFS 的影像](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="6dccb-189">顯示 HDFS 服務資訊時，請選取 [快速連結] 。</span><span class="sxs-lookup"><span data-stu-id="6dccb-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="6dccb-190">叢集前端節點的清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6dccb-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="6dccb-191">選取其中一個前端節點，然後選取 [NameNode UI] 。</span><span class="sxs-lookup"><span data-stu-id="6dccb-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![展開 [快速連結] 功能表的影像](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="6dccb-193">當您選取 [快速連結] 時，可能會出現等候指示器。</span><span class="sxs-lookup"><span data-stu-id="6dccb-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="6dccb-194">如果您的網際網路連線速度較慢，可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="6dccb-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="6dccb-195">請等候一兩分鐘，讓系統從伺服器接收資料，然後再次嘗試列出作業。</span><span class="sxs-lookup"><span data-stu-id="6dccb-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="6dccb-196">螢幕右側可能會切掉 [快速連結] 功能表中的部分項目。</span><span class="sxs-lookup"><span data-stu-id="6dccb-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="6dccb-197">若是如此，請使用滑鼠展開功能表，然後使用向右鍵將畫面捲動到右邊，以查看功能表的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="6dccb-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="6dccb-198">將會顯示與下圖類似的頁面：</span><span class="sxs-lookup"><span data-stu-id="6dccb-198">A page similar to the following image is displayed:</span></span>

    ![NameNode UI 的影像](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="6dccb-200">請注意此頁面的 URL，它應該會類似於 **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**。</span><span class="sxs-lookup"><span data-stu-id="6dccb-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="6dccb-201">此 URI 使用節點的內部完整網域名稱 (FQDN)，而且必須使用 SSH 通道才能存取。</span><span class="sxs-lookup"><span data-stu-id="6dccb-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dccb-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6dccb-202">Next steps</span></span>

<span data-ttu-id="6dccb-203">既然，您已了解如何建立和使用 SSH 通道，請參閱下列文件以了解其他使用 Ambari 的方式：</span><span class="sxs-lookup"><span data-stu-id="6dccb-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="6dccb-204">使用 Ambari 管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="6dccb-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="6dccb-205">如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="6dccb-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


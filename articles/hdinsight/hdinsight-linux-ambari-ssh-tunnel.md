---
title: "aaaUse SSH 通道 tooaccess Azure HDInsight |Microsoft 文件"
description: "了解如何 toouse SSH 通道 toosecurely 瀏覽以 Linux 為基礎的 HDInsight 節點上裝載的 web 資源。"
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
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="65d1c-103">使用 SSH 通道 tooaccess Ambari web UI、 JobHistory、 NameNode、 Oozie 和其他 web Ui</span><span class="sxs-lookup"><span data-stu-id="65d1c-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="65d1c-104">以 Linux 為基礎的 HDInsight 叢集提供透過 hello 網際網路存取 tooAmbari web UI，但 hello UI 的某些功能。</span><span class="sxs-lookup"><span data-stu-id="65d1c-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="65d1c-105">例如，hello web UI Ambari 透過其他服務。</span><span class="sxs-lookup"><span data-stu-id="65d1c-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="65d1c-106">如需完整的 hello Ambari web UI 的功能，您必須使用 SSH 通道 toohello 叢集標頭。</span><span class="sxs-lookup"><span data-stu-id="65d1c-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="65d1c-107">為何要使用 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="65d1c-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="65d1c-108">有幾個 Ambari hello 功能表只可透過 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="65d1c-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="65d1c-109">這些功能表依賴其他節點類型上執行的網站和服務，例如背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="65d1c-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="65d1c-110">通常，這些網站並未受到保護，因此並不安全的 toodirectly 公開它們在 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="65d1c-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="65d1c-111">下列 Web Ui 的 hello 需要 SSH 通道：</span><span class="sxs-lookup"><span data-stu-id="65d1c-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="65d1c-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="65d1c-112">JobHistory</span></span>
* <span data-ttu-id="65d1c-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="65d1c-113">NameNode</span></span>
* <span data-ttu-id="65d1c-114">執行緒堆疊</span><span class="sxs-lookup"><span data-stu-id="65d1c-114">Thread Stacks</span></span>
* <span data-ttu-id="65d1c-115">Oozie Web UI</span><span class="sxs-lookup"><span data-stu-id="65d1c-115">Oozie web UI</span></span>
* <span data-ttu-id="65d1c-116">HBase Master 和記錄 UI</span><span class="sxs-lookup"><span data-stu-id="65d1c-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="65d1c-117">如果您使用指令碼動作 toocustomize 您的叢集時，任何服務或公用程式安裝會公開 web UI 要求的 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="65d1c-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="65d1c-118">例如，如果您安裝使用指令碼動作色調，您必須使用 SSH 通道 tooaccess hello 色調 web UI。</span><span class="sxs-lookup"><span data-stu-id="65d1c-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65d1c-119">如果您有直接存取 tooHDInsight 透過虛擬網路，您不需要 toouse SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="65d1c-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="65d1c-120">如需直接存取 HDInsight 透過虛擬網路的範例，請參閱 hello[連接 HDInsight tooyour 在內部部署網路](connect-on-premises-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="65d1c-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="65d1c-121">什麼是 SSH 通道</span><span class="sxs-lookup"><span data-stu-id="65d1c-121">What is an SSH tunnel</span></span>

<span data-ttu-id="65d1c-122">[安全殼層 (SSH) 通道](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling)tooa 連接埠傳送您的本機工作站上的流量路由傳送。</span><span class="sxs-lookup"><span data-stu-id="65d1c-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="65d1c-123">hello 流量路由傳送透過 SSH 連線 tooyour HDInsight 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="65d1c-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="65d1c-124">hello 要求會解析，如同原始程式碼 hello 前端節點上。</span><span class="sxs-lookup"><span data-stu-id="65d1c-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="65d1c-125">hello 回應 hello 通道 tooyour 工作站透過回傳然後路由傳送。</span><span class="sxs-lookup"><span data-stu-id="65d1c-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65d1c-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="65d1c-126">Prerequisites</span></span>

* <span data-ttu-id="65d1c-127">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="65d1c-127">An SSH client.</span></span> <span data-ttu-id="65d1c-128">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="65d1c-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="65d1c-129">可以是網頁瀏覽器設定 toouse SOCKS5 proxy。</span><span class="sxs-lookup"><span data-stu-id="65d1c-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="65d1c-130">hello SOCKS proxy 支援內建於 Windows 不支援 SOCKS5，而且不適用於這份文件中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="65d1c-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="65d1c-131">hello 下列瀏覽器依賴 Windows proxy 設定，並目前並不是使用這份文件中的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="65d1c-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="65d1c-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="65d1c-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="65d1c-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="65d1c-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="65d1c-134">Google Chrome 也依賴 Windows hello 的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="65d1c-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="65d1c-135">不過，您可以安裝支援 SOCKS5 的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="65d1c-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="65d1c-136">我們建議使用 [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp)。</span><span class="sxs-lookup"><span data-stu-id="65d1c-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="65d1c-137"><a name="usessh"></a>建立使用 hello SSH 命令通道</span><span class="sxs-lookup"><span data-stu-id="65d1c-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="65d1c-138">使用 hello 下列命令 toocreate SSH 通道使用 hello`ssh`命令。</span><span class="sxs-lookup"><span data-stu-id="65d1c-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="65d1c-139">取代**USERNAME**與您的 HDInsight 叢集和取代的 SSH 使用者**CLUSTERNAME** hello 您的 HDInsight 叢集名稱：</span><span class="sxs-lookup"><span data-stu-id="65d1c-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="65d1c-140">此命令會建立路由流量 toolocal 連接埠 9876 toohello 叢集透過 SSH 的連接。</span><span class="sxs-lookup"><span data-stu-id="65d1c-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="65d1c-141">hello 選項如下：</span><span class="sxs-lookup"><span data-stu-id="65d1c-141">hello options are:</span></span>

* <span data-ttu-id="65d1c-142">**D 9876** -hello 路由傳送流量透過 hello 通道的本機連接埠。</span><span class="sxs-lookup"><span data-stu-id="65d1c-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="65d1c-143">**C** - 壓縮所有資料，因為網路流量大多是文字。</span><span class="sxs-lookup"><span data-stu-id="65d1c-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="65d1c-144">**2** -force SSH tootry 通訊協定版本 2 只。</span><span class="sxs-lookup"><span data-stu-id="65d1c-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="65d1c-145">**q** - 無訊息模式。</span><span class="sxs-lookup"><span data-stu-id="65d1c-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="65d1c-146">**T** - 停用虛擬 tty 配置，因為我們只是轉送連接埠。</span><span class="sxs-lookup"><span data-stu-id="65d1c-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="65d1c-147">**n** - 防止讀取 STDIN，因為我們只是轉送連接埠。</span><span class="sxs-lookup"><span data-stu-id="65d1c-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="65d1c-148">**N** - 不執行遠端命令，因為我們只是轉送連接埠。</span><span class="sxs-lookup"><span data-stu-id="65d1c-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="65d1c-149">**f** -hello 背景中執行。</span><span class="sxs-lookup"><span data-stu-id="65d1c-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="65d1c-150">一旦 hello 命令完成時，傳送的流量 tooport 9876 hello 本機電腦上就是路由的 toohello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="65d1c-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="65d1c-151"><a name="useputty"></a>使用 PuTTY 建立通道</span><span class="sxs-lookup"><span data-stu-id="65d1c-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="65d1c-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) 是適用於 Windows 的圖形化 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="65d1c-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="65d1c-153">使用下列步驟 toocreate SSH 通道使用 PuTTY hello:</span><span class="sxs-lookup"><span data-stu-id="65d1c-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="65d1c-154">開啟 PuTTY，並輸入連線資訊。</span><span class="sxs-lookup"><span data-stu-id="65d1c-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="65d1c-155">如果您不熟悉 PuTTY，請參閱 hello [PuTTY 文件 (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)。</span><span class="sxs-lookup"><span data-stu-id="65d1c-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="65d1c-156">在 hello**類別**區段 toohello 方 hello 對話方塊中，展開**連接**，依序展開**SSH**，然後選取**通道**。</span><span class="sxs-lookup"><span data-stu-id="65d1c-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="65d1c-157">提供下列資訊在 hello hello**選項控制 SSH 連接埠轉送**表單：</span><span class="sxs-lookup"><span data-stu-id="65d1c-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="65d1c-158">**來源連接埠**-hello 想 tooforward hello 用戶端上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="65d1c-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="65d1c-159">例如， **9876**。</span><span class="sxs-lookup"><span data-stu-id="65d1c-159">For example, **9876**.</span></span>

   * <span data-ttu-id="65d1c-160">**目的地**-hello hello 以 Linux 為基礎的 HDInsight 叢集的 SSH 位址。</span><span class="sxs-lookup"><span data-stu-id="65d1c-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="65d1c-161">例如， **mycluster-ssh.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="65d1c-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="65d1c-162">**動態** - 啟用動態 SOCKS Proxy 路由。</span><span class="sxs-lookup"><span data-stu-id="65d1c-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![通道處理選項的影像](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="65d1c-164">按一下**新增**tooadd hello 設定，然後按一下**開啟**tooopen SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="65d1c-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="65d1c-165">出現提示時，登入 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="65d1c-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="65d1c-166">使用從您的瀏覽器的 hello 通道</span><span class="sxs-lookup"><span data-stu-id="65d1c-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65d1c-167">hello 依這個區段使用 hello Mozilla FireFox 瀏覽器中，因為它在所有平台之間提供 hello 相同的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="65d1c-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="65d1c-168">其他的新式瀏覽器，例如 Google Chrome，可能需要等 FoxyProxy toowork hello 通道與擴充功能。</span><span class="sxs-lookup"><span data-stu-id="65d1c-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="65d1c-169">設定 hello 瀏覽器 toouse **localhost**和 hello 時使用的連接埠建立 hello 通道為**SOCKS v5** proxy。</span><span class="sxs-lookup"><span data-stu-id="65d1c-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="65d1c-170">Hello Firefox 設定看起來如下。</span><span class="sxs-lookup"><span data-stu-id="65d1c-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="65d1c-171">如果您使用不同的通訊埠，比 9876，變更您所使用的 hello 連接埠 toohello:</span><span class="sxs-lookup"><span data-stu-id="65d1c-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![Firefox 設定的影像](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="65d1c-173">選取**遠端 DNS**解析網域名稱系統 (DNS) 要求使用 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="65d1c-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="65d1c-174">這項設定會解析 DNS 使用 hello hello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="65d1c-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="65d1c-175">請確認該 hello 通道的運作方式是瀏覽網站時，例如[http://www.whatismyip.com/](http://www.whatismyip.com/)。</span><span class="sxs-lookup"><span data-stu-id="65d1c-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="65d1c-176">hello IP 傳回其中一個應由 hello Microsoft Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="65d1c-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="65d1c-177">驗證 Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="65d1c-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="65d1c-178">一旦建立 hello 叢集中，使用下列步驟，您可以從 hello Ambari Web 存取服務 web Ui 的 tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="65d1c-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="65d1c-179">在您的瀏覽器，移 toohttp://headnodehost:8080。</span><span class="sxs-lookup"><span data-stu-id="65d1c-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="65d1c-180">hello`headnodehost`位址是透過傳送 hello 通道 toohello 叢集，然後解決 toohello 叢集前端節點上執行 Ambari。</span><span class="sxs-lookup"><span data-stu-id="65d1c-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="65d1c-181">出現提示時，輸入 hello 系統管理員使用者名稱 （管理員） 和密碼為您的叢集。</span><span class="sxs-lookup"><span data-stu-id="65d1c-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="65d1c-182">您可能會提示輸入第二次 hello Ambari web UI。</span><span class="sxs-lookup"><span data-stu-id="65d1c-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="65d1c-183">若是如此，重新輸入 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="65d1c-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="65d1c-184">當使用 hello http://headnodehost:8080 位址 tooconnect toohello 叢集，您透過 hello 通道進行連線。</span><span class="sxs-lookup"><span data-stu-id="65d1c-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="65d1c-185">使用 hello SSH 通道，而非 HTTPS 來保護通訊。</span><span class="sxs-lookup"><span data-stu-id="65d1c-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="65d1c-186">tooconnect 超過 hello 網際網路使用 HTTPS，請使用 https://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME**是 hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="65d1c-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="65d1c-187">從 hello Ambari Web UI，請從左側的 hello 頁面 hello hello 清單中選取 HDFS。</span><span class="sxs-lookup"><span data-stu-id="65d1c-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![選取 HDFS 的影像](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="65d1c-189">顯示 hello HDFS 服務資訊時，選取**快速連結**。</span><span class="sxs-lookup"><span data-stu-id="65d1c-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="65d1c-190">Hello 叢集前端節點的清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="65d1c-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="65d1c-191">選取其中一個 hello 前端節點，然後再選取**NameNode UI**。</span><span class="sxs-lookup"><span data-stu-id="65d1c-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![展開 hello QuickLinks 功能表的映像](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="65d1c-193">當您選取 [快速連結] 時，可能會出現等候指示器。</span><span class="sxs-lookup"><span data-stu-id="65d1c-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="65d1c-194">如果您的網際網路連線速度較慢，可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="65d1c-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="65d1c-195">等候一分鐘或收到 hello 伺服器 hello 資料 toobe 的兩個，然後再試一次 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="65d1c-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="65d1c-196">某些項目在 hello**快速連結**功能表可能會切掉 hello hello 螢幕右側的。</span><span class="sxs-lookup"><span data-stu-id="65d1c-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="65d1c-197">如果是這樣，依序展開 [hello] 功能表，使用滑鼠，並使用 hello 向右箭號鍵 tooscroll hello 螢幕 toohello 右 toosee hello 的其餘部分 hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="65d1c-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="65d1c-198">會顯示下列影像頁面類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="65d1c-198">A page similar toohello following image is displayed:</span></span>

    ![Hello NameNode UI 的映像](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="65d1c-200">請注意此頁面中; hello URL它應該類似太**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/叢集**。</span><span class="sxs-lookup"><span data-stu-id="65d1c-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="65d1c-201">此 URI 使用 hello 內部完整的網域名稱 (FQDN) 的 hello 節點，而且僅可存取時使用的 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="65d1c-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65d1c-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65d1c-202">Next steps</span></span>

<span data-ttu-id="65d1c-203">既然您已經學會如何 toocreate 及使用 SSH 通道，請參閱下列文件的其他方式 toouse Ambari hello:</span><span class="sxs-lookup"><span data-stu-id="65d1c-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="65d1c-204">使用 Ambari 管理 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="65d1c-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="65d1c-205">如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="65d1c-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


---
title: "aaaCreate Jupyter/IPython 筆記型電腦 |Microsoft 文件"
description: "了解如何在 Linux 虛擬機器上的 toodeploy hello Jupyter/IPython 筆記型電腦建立 hello 資源管理員在 Azure 中的部署模型。"
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="4e071-103">在 Azure 上建立 Azure VM、安裝 Jupyter 並執行 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="4e071-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="4e071-104">hello [Jupyter 專案](http://jupyter.org)，先前稱為 hello [IPython 專案](http://ipython.org)，提供的工具集合，使用功能強大結合使用 hello 建立程式碼執行的互動式殼層科學運算即時運算文件。</span><span class="sxs-lookup"><span data-stu-id="4e071-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="4e071-105">這些 Notebook 文件可以包含任何文字、數學公式、輸入程式碼、結果、圖形、視訊，以及新型 Web 瀏覽器能夠顯示的其他任何類型的媒體。</span><span class="sxs-lookup"><span data-stu-id="4e071-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="4e071-106">您是絕對新 tooPython，且要 toolearn 有趣、 互動式環境或某些嚴重平行/技術運算、 hello Jupyter 筆記本是很好的選擇中。</span><span class="sxs-lookup"><span data-stu-id="4e071-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="4e071-107">![螢幕擷取畫面](./media/jupyter-notebook/ipy-notebook-spectral.png)使用 SciPy 和 Matplotlib 封裝 tooanalyze hello 結構的聲音錄製內容。</span><span class="sxs-lookup"><span data-stu-id="4e071-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="4e071-108">Jupyter 的兩個方法：Azure Notebook 或自訂部署</span><span class="sxs-lookup"><span data-stu-id="4e071-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="4e071-109">Azure 提供的服務，您也可以使用[快速開始使用 Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e071-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="4e071-110">藉由使用 hello Azure 筆記本服務，您可以輕鬆地取得存取 tooJupyter 可存取 web 介面的所有 hello 電源的 Python 和許多的程式庫可調整計算資源。</span><span class="sxs-lookup"><span data-stu-id="4e071-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="4e071-111">因為 hello 安裝由 hello 服務，使用者可以存取這些資源，而 hello 需要在管理和設定由 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="4e071-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="4e071-112">如果 hello 筆記本服務不適用於您案例請繼續 tooread 本文這將會顯示如何 toodeploy hello Jupyter 筆記本，Microsoft Azure 上使用 Linux 虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="4e071-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="4e071-113">在 Azure 上建立並設定 VM</span><span class="sxs-lookup"><span data-stu-id="4e071-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="4e071-114">hello 第一個步驟是 toocreate 在 Azure 上執行的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="4e071-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="4e071-115">此 VM 是 hello 雲端中的完整作業系統，並將用來執行 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="4e071-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="4e071-116">Azure 能夠執行 Linux 和 Windows 虛擬機器，並且討論 hello Jupyter 這兩種類型的虛擬機器上安裝。</span><span class="sxs-lookup"><span data-stu-id="4e071-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="4e071-117">建立 Linux VM 並開啟適用於 Jupyter 的連接埠</span><span class="sxs-lookup"><span data-stu-id="4e071-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="4e071-118">請遵循所提供的 hello 指示[這裡][ portal-vm-linux] toocreate 虛擬機器的 hello *Ubuntu*發佈。</span><span class="sxs-lookup"><span data-stu-id="4e071-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="4e071-119">本教學課程使用 Ubuntu Server 14.04 LTS。</span><span class="sxs-lookup"><span data-stu-id="4e071-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="4e071-120">我們假設 hello 使用者名*azureuser*。</span><span class="sxs-lookup"><span data-stu-id="4e071-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="4e071-121">Hello 虛擬機器部署之後，我們必須 tooopen 向上 hello 網路安全性群組安全性規則。</span><span class="sxs-lookup"><span data-stu-id="4e071-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="4e071-122">從 hello Azure 入口網站，移過**網路安全性群組**和開啟 hello hello 安全性群組對應 tooyour VM 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4e071-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="4e071-123">您需要 tooadd 輸入安全性規則以 hello 下列設定： **TCP** hello 通訊協定，  **\***  hello 來源 （公用） 連接埠和**9999**的hello （私人） 目的地連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e071-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="4e071-125">在您網路的安全性群組，而按一下**網路介面**和附註 hello**公用 IP 位址**因為 hello 下一個步驟中將需要的 tooconnect tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="4e071-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="4e071-126">在 hello VM 上安裝必要的軟體</span><span class="sxs-lookup"><span data-stu-id="4e071-126">Install required software on hello VM</span></span>
<span data-ttu-id="4e071-127">toorun hello Jupyter 筆記本我們 VM 上，我們必須先安裝 Jupyter 和其相依性。</span><span class="sxs-lookup"><span data-stu-id="4e071-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="4e071-128">連接使用 ssh tooyour linux vm，然後建立時所選擇的 hello 使用者名稱/密碼組 hello vm。</span><span class="sxs-lookup"><span data-stu-id="4e071-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="4e071-129">在本教學課程中，我們將使用 PuTTY 並從 Windows 連接。</span><span class="sxs-lookup"><span data-stu-id="4e071-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="4e071-130">在 Ubuntu 上安裝 Jupyter</span><span class="sxs-lookup"><span data-stu-id="4e071-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="4e071-131">安裝 Anaconda 的常見資料科學 python 分佈中，使用其中一種從提供的 hello 連結[Continuum Analytics](https://www.continuum.io/downloads)。</span><span class="sxs-lookup"><span data-stu-id="4e071-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="4e071-132">Hello 撰寫此文件，hello 下列連結是 hello 最向上 toodate 版本。</span><span class="sxs-lookup"><span data-stu-id="4e071-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="4e071-133">適用於 Linux 的 Anaconda 安裝</span><span class="sxs-lookup"><span data-stu-id="4e071-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="4e071-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="4e071-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="4e071-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="4e071-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="4e071-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="4e071-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="4e071-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="4e071-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="4e071-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="4e071-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="4e071-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="4e071-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="4e071-140">在 Ubuntu 上安裝 Anaconda3 2.3.0 64 位元</span><span class="sxs-lookup"><span data-stu-id="4e071-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="4e071-141">例如，這是您可以在 Ubuntu 上安裝 Anaconda 的方式</span><span class="sxs-lookup"><span data-stu-id="4e071-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![螢幕擷取畫面](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="4e071-143">設定 Jupyter 並使用 SSL</span><span class="sxs-lookup"><span data-stu-id="4e071-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="4e071-144">在安裝之後我們需要 tootake 時刻 toosetup hello 設定檔 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="4e071-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="4e071-145">如果您遇到的問題與設定 Jupyter 可能很有幫助 toolook 在 hello [Jupyter 筆記本 Server 文件](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html)。</span><span class="sxs-lookup"><span data-stu-id="4e071-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="4e071-146">下一步我們`cd`toohello 設定檔目錄 toocreate 我們的 SSL 憑證，然後編輯 hello 設定檔組態檔。</span><span class="sxs-lookup"><span data-stu-id="4e071-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="4e071-147">在 Linux 上使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e071-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="4e071-148">使用下列命令 toocreate hello SSL 憑證 （Linux 和 Windows） 的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e071-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="4e071-149">請注意，由於連接 toohello 筆記本時，我們會建立自我簽署的 SSL 憑證，您的瀏覽器會提供您的安全性警告。</span><span class="sxs-lookup"><span data-stu-id="4e071-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="4e071-150">用於長期實際執行環境，您會想 toouse 正確簽署的憑證與您的組織相關聯。</span><span class="sxs-lookup"><span data-stu-id="4e071-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="4e071-151">由於憑證管理超出範圍 hello 這個示範中，我們將著重 tooa 自我簽署的憑證現在。</span><span class="sxs-lookup"><span data-stu-id="4e071-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="4e071-152">此外 toousing 憑證，您必須也提供密碼 tooprotect 筆記本免於未經授權使用。</span><span class="sxs-lookup"><span data-stu-id="4e071-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="4e071-153">基於安全性理由 Jupyter 加密的密碼，其組態檔中，因此您需要 tooencrypt 密碼會先使用。</span><span class="sxs-lookup"><span data-stu-id="4e071-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="4e071-154">IPython 提供公用程式 toodo，;在命令提示字元執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e071-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="4e071-155">這會提示您輸入密碼和確認訊息，並將然後列印 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="4e071-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="4e071-156">請注意此步驟之後的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e071-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="4e071-157">接下來，我們將在其中編輯 hello 設定檔的組態檔，也就是`jupyter_notebook_config.py`您是在 hello 目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="4e071-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="4e071-158">請注意，這個檔案可能不存在-在 hello 情形下直接建立。</span><span class="sxs-lookup"><span data-stu-id="4e071-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="4e071-159">此檔案有許多欄位，預設為注釋排除所有欄位。您可以使用您慣用的任何文字編輯器開啟這個檔案，您應該確定至少有 hello 下列內容。</span><span class="sxs-lookup"><span data-stu-id="4e071-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="4e071-160">**會在與 hello 先前步驟中的 hello sha1 hello 組態中的確定 tooreplace hello c.NotebookApp.password**。</span><span class="sxs-lookup"><span data-stu-id="4e071-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="4e071-161">執行 hello Jupyter 筆記本</span><span class="sxs-lookup"><span data-stu-id="4e071-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="4e071-162">此時我們已經準備好 toostart hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="4e071-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="4e071-163">toodo，瀏覽您想 toostore 筆記本，並以下列命令的 hello 啟動 hello Jupyter 筆記本伺服器 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="4e071-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="4e071-164">您現在應該會無法 tooaccess Jupyter 筆記本 hello 位址`https://[PUBLIC-IP-ADDRESS]:9999`。</span><span class="sxs-lookup"><span data-stu-id="4e071-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="4e071-165">當您第一次存取筆記本時，hello 登入頁面會要求您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="4e071-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="4e071-166">一旦您登入，您會看到 hello"Jupyter 筆記本儀表板 」，這是所有筆記本作業下時中心。</span><span class="sxs-lookup"><span data-stu-id="4e071-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="4e071-167">從此頁面中，您可以建立新 Notebook 和開啟現有 Notebook。</span><span class="sxs-lookup"><span data-stu-id="4e071-167">From this page you can create new notebooks and open existing ones.</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="4e071-169">使用 hello Jupyter 筆記本</span><span class="sxs-lookup"><span data-stu-id="4e071-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="4e071-170">如果您按一下 hello**新增** 按鈕，您會看到下列開啟頁面上的 hello。</span><span class="sxs-lookup"><span data-stu-id="4e071-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="4e071-172">hello 區域標記為`In []:`提示是 hello 輸入的區域中，您可以在這裡輸入有效的 Python 程式碼，且當您叫用時，它會執行`Shift-Enter`或按一下 hello 「 播放 」 圖示 （hello 指向右方的三角形 hello 工具列中）。</span><span class="sxs-lookup"><span data-stu-id="4e071-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="4e071-173">強大的典範：具有多樣化媒體的即時運算文件</span><span class="sxs-lookup"><span data-stu-id="4e071-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="4e071-174">hello 筆記本本身應該覺得很自然 tooanyone Python 和文書處理器，已使用的使用者，因為它是在某些方面兩者的混合： 您可以執行 Python 程式碼區塊，但您也可以讓便箋及其他文字，藉由變更從 「 程式碼 」 儲存格樣式 hello 太"Markdown 」 使用工具列中的 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="4e071-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="4e071-175">Jupyter 不只是文字處理器，因為它能夠混合運算和多樣化媒體 (文字、圖形、視訊及新型網頁瀏覽器可以顯示的任何內容)。</span><span class="sxs-lookup"><span data-stu-id="4e071-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="4e071-176">您可以混合文字、程式碼、影片及更多項目！</span><span class="sxs-lookup"><span data-stu-id="4e071-176">You can mix, text, code, videos and more!</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="4e071-178">可以使用相同簡化為複雜的網路分析，在其中一種環境中的 hello 執行簡單的計算與 Python 的許多絕佳的程式庫用於科學運算，hello 下列螢幕擷取畫面中的 hello 電源。</span><span class="sxs-lookup"><span data-stu-id="4e071-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="4e071-179">此範例與即時計算混合的 hello 新式 web hello 電源提供許多的可能性，和最適合 hello 雲端;hello 筆記本可以用於：</span><span class="sxs-lookup"><span data-stu-id="4e071-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="4e071-180">探勘測試計算手寫板 toorecord 為處理問題。</span><span class="sxs-lookup"><span data-stu-id="4e071-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="4e071-181">與同事 '即時' 的計算表單中或硬拷貝格式 （HTML、 PDF） 會產生 tooshare。</span><span class="sxs-lookup"><span data-stu-id="4e071-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="4e071-182">toodistribute 存在即時教學資料牽涉到計算，因此學生可以立即試驗 hello 真正的程式碼，進行修改並以互動方式重新執行。</span><span class="sxs-lookup"><span data-stu-id="4e071-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="4e071-183">tooprovide"可執行檔白皮書"，都可以立即重新產生，而沒有 hello 結果的參考資料進行驗證，並由其他擴充。</span><span class="sxs-lookup"><span data-stu-id="4e071-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="4e071-184">做為計算的共同作業平台： 多個使用者可以登入 toothe 相同的筆記本伺服器 tooshare 即時計算的工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e071-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="4e071-185">如果您 IPython 原始程式碼 toohello[儲存機制][repository]，您會發現使用筆記本的範例，其中您可以下載並在您自己的 Azure Jupyter VM 然後試驗整個目錄。</span><span class="sxs-lookup"><span data-stu-id="4e071-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="4e071-186">只要下載 hello`.ipynb`檔案 hello 從站台和將它們上傳到 Azure VM 筆記本的 hello 儀表板 （或直接在 hello VM 下載它們）。</span><span class="sxs-lookup"><span data-stu-id="4e071-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="4e071-187">結論</span><span class="sxs-lookup"><span data-stu-id="4e071-187">Conclusion</span></span>
<span data-ttu-id="4e071-188">hello Jupyter 筆記本提供功能強大的介面存取以互動方式在 Azure 上的 hello Python 生態系統的 hello 電源。</span><span class="sxs-lookup"><span data-stu-id="4e071-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="4e071-189">它涵蓋的用途範圍相當廣泛，包括簡單的探究和學習 Python、資料分析和視覺化、模擬和平行運算。</span><span class="sxs-lookup"><span data-stu-id="4e071-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="4e071-190">hello 產生筆記本文件包含 hello 計算會執行，而且可以與其他 Jupyter 使用者共用的完整記錄。</span><span class="sxs-lookup"><span data-stu-id="4e071-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="4e071-191">hello Jupyter 筆記本可以當做本機應用程式，但是它非常適合在 Azure 上的雲端部署</span><span class="sxs-lookup"><span data-stu-id="4e071-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="4e071-192">Jupyter hello 核心功能也會提供在 Visual Studio 中透過[Python Tools for Visual Studio] [ Python Tools for Visual Studio] (PTVS)。</span><span class="sxs-lookup"><span data-stu-id="4e071-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="4e071-193">PTVS 是 Microsoft 提供的免費開放原始碼外掛程式，可以將 Visual Studio 轉變為進階 Python 開發環境，其中包括具有 IntelliSense、偵錯、剖析和平行運算整合功能的進階編輯器。</span><span class="sxs-lookup"><span data-stu-id="4e071-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e071-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e071-194">Next steps</span></span>
<span data-ttu-id="4e071-195">如需詳細資訊，請參閱 hello [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="4e071-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs

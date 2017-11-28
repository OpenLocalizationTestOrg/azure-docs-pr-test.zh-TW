---
title: "建立 Jupyter/IPython Notebook | Microsoft Docs"
description: "了解如何在 Azure 中使用資源管理員部署模型建立的 Linux 虛擬機器上，部署 Jupyter/IPython Notebook。"
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
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="8652a-103">在 Azure 上建立 Azure VM、安裝 Jupyter 並執行 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="8652a-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="8652a-104">[Jupyter 專案](http://jupyter.org) (先前稱為 [IPython 專案](http://ipython.org)) 使用功能強大的互動式殼層，來提供適用於科學運算的工具集合，結合了程式碼執行與即時運算文件的建立。</span><span class="sxs-lookup"><span data-stu-id="8652a-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="8652a-105">這些 Notebook 文件可以包含任何文字、數學公式、輸入程式碼、結果、圖形、視訊，以及新型 Web 瀏覽器能夠顯示的其他任何類型的媒體。</span><span class="sxs-lookup"><span data-stu-id="8652a-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="8652a-106">無論您是第一次使用 Python 並希望在有趣的互動式環境中了解它，還是執行一些重要的平行/技術運算，Jupyter Notebook 都是相當好的選擇。</span><span class="sxs-lookup"><span data-stu-id="8652a-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="8652a-107">![螢幕擷取畫面](./media/jupyter-notebook/ipy-notebook-spectral.png) 使用 SciPy 和 Matplotlib 封裝來分析錄音的結構。</span><span class="sxs-lookup"><span data-stu-id="8652a-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="8652a-108">Jupyter 的兩個方法：Azure Notebook 或自訂部署</span><span class="sxs-lookup"><span data-stu-id="8652a-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="8652a-109">Azure 提供您可以用來 [快速開始使用 Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)的服務。</span><span class="sxs-lookup"><span data-stu-id="8652a-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="8652a-110">使用 Azure Notebook 服務，即可對具備 Python 及其許多程式庫所有功能的可調整運算資源，輕鬆獲取 Jupyter Web 存取介面的存取權。</span><span class="sxs-lookup"><span data-stu-id="8652a-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="8652a-111">由於安裝是透過服務來處理，因此，使用者可以存取這些資源，而不需依使用者進行系統管理與設定。</span><span class="sxs-lookup"><span data-stu-id="8652a-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="8652a-112">如果筆記本服務不適用您的案例，請繼續閱讀本文，本文將示範如何使用 Linux 虛擬機器 (VM)，在 Microsoft Azure 上部署 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8652a-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="8652a-113">在 Azure 上建立並設定 VM</span><span class="sxs-lookup"><span data-stu-id="8652a-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="8652a-114">第一步是建立在 Azure 上運作的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="8652a-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="8652a-115">此 VM 是雲端中的完整作業系統，它將用來執行 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8652a-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="8652a-116">Azure 能夠同時執行 Linux 和 Windows 虛擬機器，而我們將介紹如何在這兩種類型的虛擬機器上設定 Jupyter。</span><span class="sxs-lookup"><span data-stu-id="8652a-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="8652a-117">建立 Linux VM 並開啟適用於 Jupyter 的連接埠</span><span class="sxs-lookup"><span data-stu-id="8652a-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="8652a-118">按照[此處][portal-vm-linux]提供的指示來建立 *Ubuntu* 散發套件的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8652a-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="8652a-119">本教學課程使用 Ubuntu Server 14.04 LTS。</span><span class="sxs-lookup"><span data-stu-id="8652a-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="8652a-120">我們假設預設使用者名稱是 *azureuser*。</span><span class="sxs-lookup"><span data-stu-id="8652a-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="8652a-121">部署虛擬機器之後，我們需要開啟關於網路安全性群組的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="8652a-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="8652a-122">從 Azure 入口網站移至 [網路安全性群組]，然後開啟對應到您 VM 的安全性群組索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8652a-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="8652a-123">您必須使用下列設定來新增輸入安全性規則：針對通訊協定輸入 **TCP**、針對來源 (公用) 連接埠輸入 **\***，以及針對目的地 (私人) 連接埠輸入 **9999**。</span><span class="sxs-lookup"><span data-stu-id="8652a-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="8652a-125">在網路安全性群組中，按一下 [網路介面]，並記下**公用 IP 位址**，您在下一步驟中連接到 VM 時需要用到此位址。</span><span class="sxs-lookup"><span data-stu-id="8652a-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="8652a-126">在 VM 上安裝必要軟體</span><span class="sxs-lookup"><span data-stu-id="8652a-126">Install required software on the VM</span></span>
<span data-ttu-id="8652a-127">若要在我們的 VM 上執行 Jupyter Notebook，必須先安裝 Jupyter 及其相依性。</span><span class="sxs-lookup"><span data-stu-id="8652a-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="8652a-128">使用 ssh 以及您在建立 VM 時選擇的使用者名稱/密碼組，連接到您的 linux vm。</span><span class="sxs-lookup"><span data-stu-id="8652a-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="8652a-129">在本教學課程中，我們將使用 PuTTY 並從 Windows 連接。</span><span class="sxs-lookup"><span data-stu-id="8652a-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="8652a-130">在 Ubuntu 上安裝 Jupyter</span><span class="sxs-lookup"><span data-stu-id="8652a-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="8652a-131">使用 [Continuum Analytics](https://www.continuum.io/downloads)提供的其中一個連結來安裝 Anaconda，此為常用的資料科學 Python 散發套件。</span><span class="sxs-lookup"><span data-stu-id="8652a-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="8652a-132">撰寫本文件時，下列連結是最新日期的版本。</span><span class="sxs-lookup"><span data-stu-id="8652a-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="8652a-133">適用於 Linux 的 Anaconda 安裝</span><span class="sxs-lookup"><span data-stu-id="8652a-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="8652a-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="8652a-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="8652a-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="8652a-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="8652a-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="8652a-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="8652a-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="8652a-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8652a-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="8652a-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="8652a-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 位元</href>
    </span><span class="sxs-lookup"><span data-stu-id="8652a-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="8652a-140">在 Ubuntu 上安裝 Anaconda3 2.3.0 64 位元</span><span class="sxs-lookup"><span data-stu-id="8652a-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="8652a-141">例如，這是您可以在 Ubuntu 上安裝 Anaconda 的方式</span><span class="sxs-lookup"><span data-stu-id="8652a-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![螢幕擷取畫面](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="8652a-143">設定 Jupyter 並使用 SSL</span><span class="sxs-lookup"><span data-stu-id="8652a-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="8652a-144">安裝之後，我們需要花點時間，針對 Jupyter 安裝組態檔。</span><span class="sxs-lookup"><span data-stu-id="8652a-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="8652a-145">如果您在設定 Jupyter 時遇到麻煩，查看 [適用於執行 Notebook 伺服器的 Jupyter 文件](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html)可能會有幫助。</span><span class="sxs-lookup"><span data-stu-id="8652a-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="8652a-146">然後，透過 `cd` 切換到設定檔目錄，來建立 SSL 憑證並編輯設定檔組態檔案。</span><span class="sxs-lookup"><span data-stu-id="8652a-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="8652a-147">在 Linux 上使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="8652a-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="8652a-148">使用下列命令建立 SSL 憑證 (Linux 和 Windows)。</span><span class="sxs-lookup"><span data-stu-id="8652a-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="8652a-149">請注意，由於我們建立的是自我簽署 SSL 憑證，因此在連線至 Notebook 時，您的瀏覽器將發出安全性警告。</span><span class="sxs-lookup"><span data-stu-id="8652a-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="8652a-150">若要進行長期生產使用，您將需要使用與您的組織相關聯的正確簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="8652a-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="8652a-151">由於憑證管理不在本展示的範圍，因此目前只討論自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="8652a-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="8652a-152">除了使用憑證之外，您也必須提供密碼，以防未經授權而使用您的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="8652a-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="8652a-153">基於安全考量，Jupyter 會在其組態檔中使用加密密碼，因此您需要先加密您的密碼。</span><span class="sxs-lookup"><span data-stu-id="8652a-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="8652a-154">IPython 提供一個公用程式來進行此作業；在命令提示字元下，執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="8652a-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="8652a-155">這將提示您提供密碼並確認，接著將會顯示密碼。</span><span class="sxs-lookup"><span data-stu-id="8652a-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="8652a-156">請記下此密碼，以便在下一個步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="8652a-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="8652a-157">接著，我們將編輯設定檔的組態檔，也就是您所在目錄中的 `jupyter_notebook_config.py` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8652a-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="8652a-158">請注意，這個檔案可能不存在 -- 如果不存在，只需建立它即可。</span><span class="sxs-lookup"><span data-stu-id="8652a-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="8652a-159">此檔案有許多欄位，預設為注釋排除所有欄位。</span><span class="sxs-lookup"><span data-stu-id="8652a-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="8652a-160">您可以使用您喜好的任何文字編輯器開啟此檔案，並且應該確保其中至少有以下內容。</span><span class="sxs-lookup"><span data-stu-id="8652a-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="8652a-161">**請務必使用前一個步驟中的 sha1 來取代 config 中的 c.NotebookApp.password**。</span><span class="sxs-lookup"><span data-stu-id="8652a-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="8652a-162">執行 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="8652a-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="8652a-163">此時，我們已準備好啟動 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8652a-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="8652a-164">若要這麼做，請瀏覽至您想要在其中儲存 Notebook 的目錄，並使用下列命令來啟動 Jupyter Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8652a-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="8652a-165">您現在應該可以在 `https://[PUBLIC-IP-ADDRESS]:9999`的網址中存取您的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8652a-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="8652a-166">您第一次存取 Notebook 時，登入頁面會詢問您的密碼。</span><span class="sxs-lookup"><span data-stu-id="8652a-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="8652a-167">登入後，您會看見「Jupyter Notebook 儀表板」，它是所有 Notebook 作業的控制中心。</span><span class="sxs-lookup"><span data-stu-id="8652a-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="8652a-168">從此頁面中，您可以建立新 Notebook 和開啟現有 Notebook。</span><span class="sxs-lookup"><span data-stu-id="8652a-168">From this page you can create new notebooks and open existing ones.</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="8652a-170">使用 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="8652a-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="8652a-171">如果按一下 [新增]  按鈕，您將看到以下開啟頁面。</span><span class="sxs-lookup"><span data-stu-id="8652a-171">If you click the **New** button, you will see the following opening page.</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="8652a-173">標記有 `In []:` 提示的區域是輸入區域，您可以在其中輸入任何有效的 Python 程式碼，而它會在您按 `Shift-Enter` 鍵或按一下 [播放] 圖示 (工具欄中的向右三角形) 時執行。</span><span class="sxs-lookup"><span data-stu-id="8652a-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="8652a-174">強大的典範：具有多樣化媒體的即時運算文件</span><span class="sxs-lookup"><span data-stu-id="8652a-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="8652a-175">Notebook 本身對曾經使用 Python 和文字處理器的人而言應該感覺相當自然，因為它在某些方面是這兩者的結合：您可以執行 Python 程式碼區塊，但是也可以使用工具列中的下拉式功能表，將儲存格的樣式從 [程式碼] 更改為 [Markdown] 來保留記事及其他文字。</span><span class="sxs-lookup"><span data-stu-id="8652a-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="8652a-176">Jupyter 不只是文字處理器，因為它能夠混合運算和多樣化媒體 (文字、圖形、視訊及新型網頁瀏覽器可以顯示的任何內容)。</span><span class="sxs-lookup"><span data-stu-id="8652a-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="8652a-177">您可以混合文字、程式碼、影片及更多項目！</span><span class="sxs-lookup"><span data-stu-id="8652a-177">You can mix, text, code, videos and more!</span></span>

![螢幕擷取畫面](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="8652a-179">利用 Python 許多用於科學和科技運算的絕佳程式庫功能，在下列螢幕擷取畫面中，可進行與複雜網路分析一樣輕鬆的簡單運算，全部都在一個環境中完成。</span><span class="sxs-lookup"><span data-stu-id="8652a-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="8652a-180">這個將最新 Web 的功能與即時運算結合的典範提供許多可能性，並且相當適合雲端；Notebook 可以用來：</span><span class="sxs-lookup"><span data-stu-id="8652a-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="8652a-181">做為運算記錄器，用來記錄對於問題進行的探究工作。</span><span class="sxs-lookup"><span data-stu-id="8652a-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="8652a-182">以「即時」運算形式或檔案格式 (HTML、PDF)，與同事分享結果。</span><span class="sxs-lookup"><span data-stu-id="8652a-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="8652a-183">用於散佈和顯示涉及運算的即時教學材料，以便學生可以立即以互動方式試驗、修改和重新執行實際的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8652a-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="8652a-184">提供以可由其他人立即重現、驗證和擴展的方式顯示研究結果的「可執行文件」。</span><span class="sxs-lookup"><span data-stu-id="8652a-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="8652a-185">做為共同運算的平台：多位使用者可以登入同一部 Notebook 伺服器來共享即時運算工作階段。</span><span class="sxs-lookup"><span data-stu-id="8652a-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="8652a-186">如果您進入 IPython 原始程式碼[存放庫][repository]，將可找到提供 Notebook 範例的整個目錄，您可以下載範例，然後在自己的 Azure Jupyter VM 上進行試驗。</span><span class="sxs-lookup"><span data-stu-id="8652a-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="8652a-187">只需從網站下載 `.ipynb` 檔案，並將這些檔案上傳至您的 Notebook Azure VM 儀表板即可 (也可以將這些檔案直接下載至 VM)。</span><span class="sxs-lookup"><span data-stu-id="8652a-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="8652a-188">結論</span><span class="sxs-lookup"><span data-stu-id="8652a-188">Conclusion</span></span>
<span data-ttu-id="8652a-189">Jupyter Notebook 可為互動存取 Azure 上 Python 生態系統的功能提供強大的介面。</span><span class="sxs-lookup"><span data-stu-id="8652a-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="8652a-190">它涵蓋的用途範圍相當廣泛，包括簡單的探究和學習 Python、資料分析和視覺化、模擬和平行運算。</span><span class="sxs-lookup"><span data-stu-id="8652a-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="8652a-191">最終產生的 Notebook 文件會完整記錄已執行且能夠與其他 Jupyter 使用者共享的運算。</span><span class="sxs-lookup"><span data-stu-id="8652a-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="8652a-192">Jupyter Notebook 可以用來做為本機應用程式，不過它相當適合用於 Azure 上的雲端部署</span><span class="sxs-lookup"><span data-stu-id="8652a-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="8652a-193">您也可以透過 [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS)，在 Visual Studio 中使用 Jupyter 的核心功能。</span><span class="sxs-lookup"><span data-stu-id="8652a-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="8652a-194">PTVS 是 Microsoft 提供的免費開放原始碼外掛程式，可以將 Visual Studio 轉變為進階 Python 開發環境，其中包括具有 IntelliSense、偵錯、剖析和平行運算整合功能的進階編輯器。</span><span class="sxs-lookup"><span data-stu-id="8652a-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8652a-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8652a-195">Next steps</span></span>
<span data-ttu-id="8652a-196">如需詳細資訊，請參閱 [Python 開發人員中心](/develop/python/)。</span><span class="sxs-lookup"><span data-stu-id="8652a-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs

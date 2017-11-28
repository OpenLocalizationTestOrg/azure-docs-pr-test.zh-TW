---
title: "Azure 快速入門 - 建立 VM 入口網站 | Microsoft Docs"
description: "Azure 快速入門 - 建立 VM 入口網站"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d009020e86fdfed6a45b5b63b9664c623bcb1843
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="affb2-103">使用 Azure 入口網站建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="affb2-103">Create a Linux virtual machine with the Azure portal</span></span>

<span data-ttu-id="affb2-104">您可以透過 Azure 入口網站建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="affb2-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="affb2-105">此方法可提供以瀏覽器為基礎的使用者介面，以便建立和設定虛擬機器，以及所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="affb2-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="affb2-106">本快速入門會逐步說明如何建立虛擬機器，以及在 VM 上安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="affb2-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="affb2-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="affb2-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="affb2-108">建立 SSH 金鑰組</span><span class="sxs-lookup"><span data-stu-id="affb2-108">Create SSH key pair</span></span>

<span data-ttu-id="affb2-109">您需要有 SSH 金鑰組才能完成本快速入門。</span><span class="sxs-lookup"><span data-stu-id="affb2-109">You need an SSH key pair to complete this quick start.</span></span> <span data-ttu-id="affb2-110">如果現有的 SSH 金鑰組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="affb2-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="affb2-111">從 Bash 殼層，執行此命令並遵循畫面上的指示操作。</span><span class="sxs-lookup"><span data-stu-id="affb2-111">From a Bash shell, run this command and follow the on-screen directions.</span></span> <span data-ttu-id="affb2-112">命令輸出包含公開金鑰檔案的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="affb2-112">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="affb2-113">將公開金鑰檔案的內容複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="affb2-113">Copy the contents of the public key file to the clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a><span data-ttu-id="affb2-114">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="affb2-114">Log in to Azure</span></span> 

<span data-ttu-id="affb2-115">登入 Azure 入口網站，網址是 http://portal.azure.com/。</span><span class="sxs-lookup"><span data-stu-id="affb2-115">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="affb2-116">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="affb2-116">Create virtual machine</span></span>

1. <span data-ttu-id="affb2-117">按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="affb2-117">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="affb2-118">選取 [計算]，然後選取 [Ubuntu Server 16.04 LTS]。</span><span class="sxs-lookup"><span data-stu-id="affb2-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="affb2-119">輸入虛擬機器資訊。</span><span class="sxs-lookup"><span data-stu-id="affb2-119">Enter the virtual machine information.</span></span> <span data-ttu-id="affb2-120">針對 [驗證類型] 選取 [SSH 公開金鑰]。</span><span class="sxs-lookup"><span data-stu-id="affb2-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="affb2-121">貼上 [SSH 公開金鑰] 時，請謹慎地移除任何前置或尾端的空白字元。</span><span class="sxs-lookup"><span data-stu-id="affb2-121">When pasting in your SSH public key, take care to remove any leading or trailing white space.</span></span> <span data-ttu-id="affb2-122">完成時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="affb2-122">When complete, click **OK**.</span></span>

    ![在入口網站刀鋒視窗中輸入 VM 的基本資訊](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="affb2-124">選取 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="affb2-124">Select a size for the VM.</span></span> <span data-ttu-id="affb2-125">若要查看更多大小，請選取 [檢視全部] 或變更 [支援的磁碟類型] 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="affb2-125">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![顯示 VM 大小的螢幕擷取畫面](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="affb2-127">在 [設定] 刀鋒視窗上，保留預設值並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="affb2-127">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="affb2-128">在 [摘要] 頁面上，按一下 [確定] 來啟動虛擬機器部署。</span><span class="sxs-lookup"><span data-stu-id="affb2-128">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="affb2-129">系統會將 VM 釘選到 Azure 入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="affb2-129">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="affb2-130">一旦完成部署，VM 摘要刀鋒視窗就會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="affb2-130">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="affb2-131">連線至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="affb2-131">Connect to virtual machine</span></span>

<span data-ttu-id="affb2-132">建立虛擬機器的 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="affb2-132">Create an SSH connection with the virtual machine.</span></span>

1. <span data-ttu-id="affb2-133">按一下虛擬機器刀鋒視窗上的 [連線] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="affb2-133">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="affb2-134">[連線] 按鈕顯示的 SSH 連接字串可用來連線至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="affb2-134">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span></span>

    ![入口網站 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="affb2-136">執行以下命令來建立 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="affb2-136">Run the following command to create an SSH session.</span></span> <span data-ttu-id="affb2-137">以您從 Azure 入口網站複製的連接字串取代此連接字串。</span><span class="sxs-lookup"><span data-stu-id="affb2-137">Replace the connection string with the one you copied from the Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="affb2-138">安裝 NGINX</span><span class="sxs-lookup"><span data-stu-id="affb2-138">Install NGINX</span></span>

<span data-ttu-id="affb2-139">使用下列 bash 指令碼來更新套件來源及安裝最新的 NGINX 套件。</span><span class="sxs-lookup"><span data-stu-id="affb2-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="affb2-140">完成時，結束 SSH 工作階段並在 Azure 入口網站中傳回 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="affb2-140">When done, exit the SSH session and return the VM properties in the Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="affb2-141">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="affb2-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="affb2-142">網路安全性群組 (NSG) 可保護輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="affb2-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="affb2-143">從 Azure 入口網站建立 VM 時，會在連接埠 22 上建立 SSH 連線的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="affb2-143">When a VM is created from the Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="affb2-144">因為此 VM 託管 Web 伺服器，所以必須針對連接埠 80 建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="affb2-144">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="affb2-145">在虛擬機器上，按一下 [資源群組] 的名稱。</span><span class="sxs-lookup"><span data-stu-id="affb2-145">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="affb2-146">選取 [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="affb2-146">Select the **network security group**.</span></span> <span data-ttu-id="affb2-147">使用 [類型] 資料行可以識別 NSG。</span><span class="sxs-lookup"><span data-stu-id="affb2-147">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="affb2-148">在左側功能表的 [設定] 之下，按一下 [輸入安全性規則]。</span><span class="sxs-lookup"><span data-stu-id="affb2-148">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="affb2-149">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="affb2-149">Click on **Add**.</span></span>
5. <span data-ttu-id="affb2-150">在 [名稱] 中輸入 **http**。</span><span class="sxs-lookup"><span data-stu-id="affb2-150">In **Name**, type **http**.</span></span> <span data-ttu-id="affb2-151">確定 [連接埠範圍] 已設為 80 且 [動作] 已設為 [允許]。</span><span class="sxs-lookup"><span data-stu-id="affb2-151">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="affb2-152">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="affb2-152">Click **OK**.</span></span>


## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="affb2-153">檢視 NGINX 歡迎使用頁面</span><span class="sxs-lookup"><span data-stu-id="affb2-153">View the NGINX welcome page</span></span>

<span data-ttu-id="affb2-154">安裝 NGINX 後，且連接埠 80 對您的 VM 開啟，即可立即從網際網路存取 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="affb2-154">With NGINX installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="affb2-155">開啟 Web 瀏覽器，並輸入 VM 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="affb2-155">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="affb2-156">在 Azure 入口網站的 VM 刀鋒視窗上可找到公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="affb2-156">The public IP address can be found on the VM blade in the Azure portal.</span></span>

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="affb2-158">清除資源</span><span class="sxs-lookup"><span data-stu-id="affb2-158">Clean up resources</span></span>

<span data-ttu-id="affb2-159">若不再需要，可刪除資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="affb2-159">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="affb2-160">若要這樣做，請選取虛擬機器刀鋒視窗中的資源群組，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="affb2-160">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="affb2-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="affb2-161">Next steps</span></span>

<span data-ttu-id="affb2-162">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="affb2-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="affb2-163">若要深入了解 Azure 虛擬機器，請繼續 Linux VM 的教學課程。</span><span class="sxs-lookup"><span data-stu-id="affb2-163">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="affb2-164">Azure Linux 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="affb2-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

---
title: "如何安裝 Linux 主要目標伺服器以從 Azure 容錯移轉至內部部署 | Microsoft Docs"
description: "在重新保護 Linux 虛擬機器之前，您必須先有 Linux 主要目標伺服器。 了解如何進行安裝。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="21e76-104">安裝 Linux 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="21e76-104">Install a Linux master target server</span></span>
<span data-ttu-id="21e76-105">您可以在容錯移轉虛擬機器之後，將虛擬機器容錯回復至內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="21e76-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="21e76-106">若要進行容錯回復，您需要在從 Azure 到內部部署網站的過程中重新保護虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="21e76-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="21e76-107">針對此程序，您需要內部部署的主要目標伺服器以接收流量。</span><span class="sxs-lookup"><span data-stu-id="21e76-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="21e76-108">如果受保護的虛擬機器是 Windows 虛擬機器，您需要 Windows 主要目標。</span><span class="sxs-lookup"><span data-stu-id="21e76-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="21e76-109">若是 Linux 虛擬機器，您需要 Linux 主要目標。</span><span class="sxs-lookup"><span data-stu-id="21e76-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="21e76-110">請參閱下列步驟，以了解如何建立和安裝 Linux 主要目標。</span><span class="sxs-lookup"><span data-stu-id="21e76-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21e76-111">從主要目標伺服器的 9.10.0 版本開始，最新的主要目標伺服器只能安裝在 Ubuntu 16.04 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="21e76-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="21e76-112">CentOS6.6 伺服器上不允許安裝新的主要目標。</span><span class="sxs-lookup"><span data-stu-id="21e76-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="21e76-113">不過，您可以使用 9.10.0 版本繼續升級舊的主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="21e76-114">概觀</span><span class="sxs-lookup"><span data-stu-id="21e76-114">Overview</span></span>
<span data-ttu-id="21e76-115">本文提供如何安裝 Linux 主要目標的指示。</span><span class="sxs-lookup"><span data-stu-id="21e76-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="21e76-116">在本文末尾或 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 中張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="21e76-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21e76-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="21e76-117">Prerequisites</span></span>

* <span data-ttu-id="21e76-118">若要選擇要在其中部署主要目標的主機，請確定容錯回復的目的地是現有內部部署虛擬機器還是新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="21e76-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="21e76-119">若是現有虛擬機器，主要目標的主機應該要能存取虛擬機器的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21e76-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="21e76-120">如果內部部署虛擬機器不存在，容錯回復虛擬機器會建立在作為主要目標的相同主機上。</span><span class="sxs-lookup"><span data-stu-id="21e76-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="21e76-121">您可以選擇任何 ESXi 主機來安裝主要目標。</span><span class="sxs-lookup"><span data-stu-id="21e76-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="21e76-122">主要目標應位於可與處理序伺服器及組態伺服器通訊的網路上。</span><span class="sxs-lookup"><span data-stu-id="21e76-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="21e76-123">主要目標的版本必須等於或早於處理序伺服器和組態伺服器的版本。</span><span class="sxs-lookup"><span data-stu-id="21e76-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="21e76-124">例如，若組態伺服器的版本是 9.4，則主要目標的版本可以是 9.4 或 9.3，但不能是 9.5。</span><span class="sxs-lookup"><span data-stu-id="21e76-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="21e76-125">主要目標只能是 VMware 虛擬機器，不能是實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="21e76-126">根據大小配置準則建立主要目標</span><span class="sxs-lookup"><span data-stu-id="21e76-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="21e76-127">建立符合下列大小配置準則的主要目標：</span><span class="sxs-lookup"><span data-stu-id="21e76-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="21e76-128">**RAM**：6 GB 或更多</span><span class="sxs-lookup"><span data-stu-id="21e76-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="21e76-129">**OS 磁碟大小**：100 GB 或更多 (以安裝 CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="21e76-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="21e76-130">**用於保留磁碟機的額外磁碟大小**：1 TB</span><span class="sxs-lookup"><span data-stu-id="21e76-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="21e76-131">**CPU 核心**：4 核心或更多</span><span class="sxs-lookup"><span data-stu-id="21e76-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="21e76-132">支援下列受支援的 Ubuntu 核心。</span><span class="sxs-lookup"><span data-stu-id="21e76-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="21e76-133">核心系列</span><span class="sxs-lookup"><span data-stu-id="21e76-133">Kernel Series</span></span>  |<span data-ttu-id="21e76-134">最多支援</span><span class="sxs-lookup"><span data-stu-id="21e76-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="21e76-135">4.4</span><span class="sxs-lookup"><span data-stu-id="21e76-135">4.4</span></span>      |<span data-ttu-id="21e76-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="21e76-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="21e76-137">4.8</span><span class="sxs-lookup"><span data-stu-id="21e76-137">4.8</span></span>      |<span data-ttu-id="21e76-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="21e76-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="21e76-139">4.10</span><span class="sxs-lookup"><span data-stu-id="21e76-139">4.10</span></span>     |<span data-ttu-id="21e76-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="21e76-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="21e76-141">部署主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="21e76-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="21e76-142">安裝 Ubuntu 16.04.2 極簡版</span><span class="sxs-lookup"><span data-stu-id="21e76-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="21e76-143">請依循下列步驟以安裝 Ubuntu 16.04.2 64 位元作業系統。</span><span class="sxs-lookup"><span data-stu-id="21e76-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="21e76-144">**步驟 1：**前往[下載連結](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64)，並選擇最接近的鏡像以從中下載 Ubuntu 16.04.2 極簡版 64 位元 ISO。</span><span class="sxs-lookup"><span data-stu-id="21e76-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="21e76-145">將 Ubuntu 16.04.2 極簡版 64 位元 ISO 放在 DVD 光碟機中，並啟動系統。</span><span class="sxs-lookup"><span data-stu-id="21e76-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="21e76-146">**步驟2：**選取 [English]\(英文\) 作為慣用語言，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![選取語言](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="21e76-148">**步驟 3：**選取 [Install Ubuntu Server]\(安裝 Ubuntu 伺服器\)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![選取安裝 Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="21e76-150">**步驟 4：**選取 [English]\(英文\) 作為慣用語言，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![選取 English 作為慣用語言](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="21e76-152">**步驟 5：**從 [Time Zone]\(時區\) 選項清單中選取適當的選項，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![選取正確的時區](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="21e76-154">**步驟 6：**選取 [No]\(否\)(預設選項)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![設定鍵盤](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="21e76-156">**步驟 7：**選取 [English (US)]\(英文 (美國)\) 作為鍵盤的國家/地區，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![選取美國作為國家/地區](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="21e76-158">**步驟 8：**選取 [English (US)]\(英文 (美國)\) 作為鍵盤配置，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![選取美式英文作為鍵盤配置](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="21e76-160">**步驟 9：**在 [Hostname]\(主機名稱\) 方塊中輸入伺服器的主機名稱，然後選取 [Continue]\(繼續\)。</span><span class="sxs-lookup"><span data-stu-id="21e76-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![輸入伺服器的主機名稱](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="21e76-162">**步驟 10：**若要建立使用者帳戶，請輸入使用者名稱，然後選取 [Continue]\(繼續\)。</span><span class="sxs-lookup"><span data-stu-id="21e76-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![建立使用者帳戶](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="21e76-164">**步驟 11：**輸入新使用者帳戶的密碼，然後選取 [Continue]\(繼續\)。</span><span class="sxs-lookup"><span data-stu-id="21e76-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![輸入密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="21e76-166">**步驟 12：**確認新使用者的密碼，然後選取 [Continue]\(繼續\)。</span><span class="sxs-lookup"><span data-stu-id="21e76-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![確認密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="21e76-168">**步驟 13：**選取 [No]\(否\) (預設選項)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![設定使用者和密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="21e76-170">**步驟 14：**如果顯示的時區是正確的，選取 [Yes]\(是\) (預設選項)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="21e76-171">若要重新設定您的時區，選取 [No]\(否\)。</span><span class="sxs-lookup"><span data-stu-id="21e76-171">To reconfigure your time zone, select **No**.</span></span>

![設定時鐘](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="21e76-173">**步驟 15：**從磁碟分割方法選項中選取 [Guided - Use entire disk]\(引導式 - 使用整個磁碟\)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![選取資料分割方法選項](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="21e76-175">**步驟 16：**從 [select disk to partition]\(選取要分割的磁碟\) 選項中選擇適當的磁碟，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![選取磁碟](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="21e76-177">**步驟 17：**選取 [Yes]\(是\) 以將變更寫入至磁碟，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![將變更寫入磁碟](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="21e76-179">**步驟 18：**選取預設選項，選取 [Continue]\(繼續\)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![選取預設選項](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="21e76-181">**步驟 19：**選取適當的選項來管理您系統上的升級，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![選取如何管理升級](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="21e76-183">由於 Azure Site Recovery 主要目標伺服器需要非常特定版本的 Ubuntu，因此您需要確認已停用虛擬機器核心升級。</span><span class="sxs-lookup"><span data-stu-id="21e76-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="21e76-184">如果啟用，任何一般升級都將導致主要目標伺服器故障。</span><span class="sxs-lookup"><span data-stu-id="21e76-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="21e76-185">請確定您選取 [No automatic updates]\(不自動更新\) 選項。</span><span class="sxs-lookup"><span data-stu-id="21e76-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="21e76-186">**步驟 20：**選取預設選項。</span><span class="sxs-lookup"><span data-stu-id="21e76-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="21e76-187">如果您想要使用 openSSH 進行 SSH 連線，請選取 [OpenSSH server]\(OpenSSH 伺服器\) 選項，然後選取 [Continue]\(繼續\)。</span><span class="sxs-lookup"><span data-stu-id="21e76-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![選取軟體](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="21e76-189">**步驟 21：**選取 [Yes](是\)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![安裝 GRUB 開機載入器](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="21e76-191">**步驟 22：**選取適當的裝置以安裝開機載入器 (最好是 **/dev/sda**)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="21e76-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![選取裝置以安裝開機載入器](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="21e76-193">**步驟 23：**選取 [Continue]\(繼續\)，然後按 **Enter** 以完成安裝。</span><span class="sxs-lookup"><span data-stu-id="21e76-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![完成安裝](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="21e76-195">安裝完成後，請使用新的使用者認證登入 VM。</span><span class="sxs-lookup"><span data-stu-id="21e76-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="21e76-196">(如需詳細資訊，請參閱**步驟 10**。)</span><span class="sxs-lookup"><span data-stu-id="21e76-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="21e76-197">請依循下列螢幕擷取畫面中的描述，設定根使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="21e76-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="21e76-198">然後以根使用者的身分登入。</span><span class="sxs-lookup"><span data-stu-id="21e76-198">Then sign in as ROOT user.</span></span>

![設定根使用者的密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="21e76-200">準備要設定為主要目標伺服器的機器</span><span class="sxs-lookup"><span data-stu-id="21e76-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="21e76-201">接下來，準備要設定為主要目標伺服器的機器。</span><span class="sxs-lookup"><span data-stu-id="21e76-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="21e76-202">若要取得 Linux 虛擬機器中每個 SCSI 硬碟的識別碼，請啟用 **disk.EnableUUID = TRUE** 參數。</span><span class="sxs-lookup"><span data-stu-id="21e76-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="21e76-203">若要啟用此參數，請依循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="21e76-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="21e76-204">關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="21e76-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="21e76-205">以滑鼠右鍵按一下左窗格中的虛擬機器項目，然後選取 [Edit Settings] /(編輯設定/)。</span><span class="sxs-lookup"><span data-stu-id="21e76-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="21e76-206">選取 [選項] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="21e76-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="21e76-207">在左窗格中，選取 [進階]  >  [一般]，然後選取畫面右下方的 [組態參數] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="21e76-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![[選項] 索引標籤](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="21e76-209">[組態參數] 選項在機器執行時無法使用。</span><span class="sxs-lookup"><span data-stu-id="21e76-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="21e76-210">若要啟用此索引標籤，請關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="21e76-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="21e76-211">查看含有 [disk.EnableUUID] 的資料列是否已經存在。</span><span class="sxs-lookup"><span data-stu-id="21e76-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="21e76-212">如果該值存在，而且設定為 [False]，請將該值變更為 [True]。</span><span class="sxs-lookup"><span data-stu-id="21e76-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="21e76-213">(值不區分大小寫。)</span><span class="sxs-lookup"><span data-stu-id="21e76-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="21e76-214">如果該值存在，而且設定為 [True]，請按一下 [取消]。</span><span class="sxs-lookup"><span data-stu-id="21e76-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="21e76-215">如果該值不存在，請選取 [新增資料列]。</span><span class="sxs-lookup"><span data-stu-id="21e76-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="21e76-216">在名稱欄位中新增 **disk.EnableUUID**，然後將值設定為 [TRUE]。</span><span class="sxs-lookup"><span data-stu-id="21e76-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![檢查 disk.EnableUUID 是否已存在](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="21e76-218">停用核心升級</span><span class="sxs-lookup"><span data-stu-id="21e76-218">Disable kernel upgrades</span></span>

<span data-ttu-id="21e76-219">Azure Site Recovery 主要目標伺服器需要非常特定版本的 Ubuntu，因此請確認已停用虛擬機器的核心升級。</span><span class="sxs-lookup"><span data-stu-id="21e76-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="21e76-220">如果啟用核心升級，則任何一般升級都將導致主要目標伺服器故障。</span><span class="sxs-lookup"><span data-stu-id="21e76-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="21e76-221">下載並安裝其他套件</span><span class="sxs-lookup"><span data-stu-id="21e76-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="21e76-222">請確定您有網際網路連線以便下載並安裝其他套件。</span><span class="sxs-lookup"><span data-stu-id="21e76-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="21e76-223">若沒有網際網路連線，則必須以手動方式尋找這些 RPM 套件並加以安裝。</span><span class="sxs-lookup"><span data-stu-id="21e76-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="21e76-224">取得安裝程式</span><span class="sxs-lookup"><span data-stu-id="21e76-224">Get the installer for setup</span></span>

<span data-ttu-id="21e76-225">如果您的主要目標有網際網路連線，您可以使用下列步驟下載安裝程式。</span><span class="sxs-lookup"><span data-stu-id="21e76-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="21e76-226">否則，您可以從處理序伺服器複製安裝程式並加以安裝。</span><span class="sxs-lookup"><span data-stu-id="21e76-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="21e76-227">下載主要目標安裝套件</span><span class="sxs-lookup"><span data-stu-id="21e76-227">Download the master target installation packages</span></span>

<span data-ttu-id="21e76-228">[下載最新的 Linux 主要目標安裝位元](https://aka.ms/latestlinuxmobsvc)。</span><span class="sxs-lookup"><span data-stu-id="21e76-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="21e76-229">若要使用 Linux 下載它，請輸入：</span><span class="sxs-lookup"><span data-stu-id="21e76-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="21e76-230">請務必在主目錄中下載並解壓縮安裝程式。</span><span class="sxs-lookup"><span data-stu-id="21e76-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="21e76-231">如果您解壓縮至 **/usr/Local**，安裝將會失敗。</span><span class="sxs-lookup"><span data-stu-id="21e76-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="21e76-232">從處理序伺服器存取安裝程式</span><span class="sxs-lookup"><span data-stu-id="21e76-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="21e76-233">在處理序伺服器上，移至 **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**。</span><span class="sxs-lookup"><span data-stu-id="21e76-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="21e76-234">從處理序伺服器複製必要的安裝程式檔案，並在主目錄中將其儲存為 **latestlinuxmobsvc.tar.gz**。</span><span class="sxs-lookup"><span data-stu-id="21e76-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="21e76-235">套用自訂組態變更</span><span class="sxs-lookup"><span data-stu-id="21e76-235">Apply custom configuration changes</span></span>

<span data-ttu-id="21e76-236">若要套用自訂組態變更，請使用下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="21e76-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="21e76-237">執行下列命令來解壓縮二進位檔。</span><span class="sxs-lookup"><span data-stu-id="21e76-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![所執行命令的螢幕擷取畫面](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="21e76-239">執行下列命令來授與權限。</span><span class="sxs-lookup"><span data-stu-id="21e76-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="21e76-240">執行下列命令來執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="21e76-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="21e76-241">只需在伺服器上執行指令碼一次。</span><span class="sxs-lookup"><span data-stu-id="21e76-241">Run the script only once on the server.</span></span> <span data-ttu-id="21e76-242">關閉伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-242">Shut down the server.</span></span> <span data-ttu-id="21e76-243">然後，如下節中所述新增磁碟後，重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="21e76-244">將保留磁碟新增至 Linux 主要目標虛擬機器</span><span class="sxs-lookup"><span data-stu-id="21e76-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="21e76-245">使用下列步驟來建立保留磁碟：</span><span class="sxs-lookup"><span data-stu-id="21e76-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="21e76-246">將新的 1-TB 磁碟連結至 Linux 主要目標虛擬機器，然後啟動機器。</span><span class="sxs-lookup"><span data-stu-id="21e76-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="21e76-247">使用 **multipath -ll** 命令以便得知保留磁碟的多重路徑識別碼。</span><span class="sxs-lookup"><span data-stu-id="21e76-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![保留磁碟的多重路徑識別碼](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="21e76-249">格式化磁碟機，並在新的磁碟機上建立檔案系統。</span><span class="sxs-lookup"><span data-stu-id="21e76-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![在磁碟機上建立檔案系統](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="21e76-251">建立檔案系統之後，掛接保留磁碟。</span><span class="sxs-lookup"><span data-stu-id="21e76-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![掛接保留磁碟](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="21e76-253">建立 **fstab** 項目，以便在每次啟動系統時掛接保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="21e76-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="21e76-254">按 **Insert** 鍵來開始編輯檔案。</span><span class="sxs-lookup"><span data-stu-id="21e76-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="21e76-255">建立新的一行，並插入下列文字。</span><span class="sxs-lookup"><span data-stu-id="21e76-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="21e76-256">根據前一個命令中醒目提示的多重路徑識別碼，編輯磁碟多重路徑識別碼。</span><span class="sxs-lookup"><span data-stu-id="21e76-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="21e76-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="21e76-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="21e76-258">按 **Esc** 鍵，然後輸入 **:wq** (寫入和結束)，以關閉編輯器視窗。</span><span class="sxs-lookup"><span data-stu-id="21e76-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="21e76-259">安裝主要目標</span><span class="sxs-lookup"><span data-stu-id="21e76-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21e76-260">主要目標伺服器的版本必須等於或早於處理序伺服器和組態伺服器的版本。</span><span class="sxs-lookup"><span data-stu-id="21e76-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="21e76-261">如果不符合此條件，重新保護會成功，但複寫會失敗。</span><span class="sxs-lookup"><span data-stu-id="21e76-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="21e76-262">在安裝主要目標伺服器之前，請確認虛擬機器上的 **/etc/hosts** 檔案包含會將本機主機名稱對應到所有網路介面卡相關 IP 位址的項目。</span><span class="sxs-lookup"><span data-stu-id="21e76-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="21e76-263">在組態伺服器上從 **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** 複製複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="21e76-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="21e76-264">然後執行下列命令，將其儲存在同個本機目錄中的 **passphrase.txt**：</span><span class="sxs-lookup"><span data-stu-id="21e76-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="21e76-265">範例：</span><span class="sxs-lookup"><span data-stu-id="21e76-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="21e76-266">記下組態伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="21e76-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="21e76-267">您在下一步需要用到它。</span><span class="sxs-lookup"><span data-stu-id="21e76-267">You need it in the next step.</span></span>

3. <span data-ttu-id="21e76-268">執行下列命令來安裝主要目標伺服器，並向組態伺服器註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="21e76-269">範例：</span><span class="sxs-lookup"><span data-stu-id="21e76-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="21e76-270">等候指令碼完成。</span><span class="sxs-lookup"><span data-stu-id="21e76-270">Wait until the script finishes.</span></span> <span data-ttu-id="21e76-271">如果主要目標註冊成功，主要目標會列在入口網站的 [Site Recovery 基礎結構] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="21e76-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="21e76-272">使用互動式安裝來安裝主要目標</span><span class="sxs-lookup"><span data-stu-id="21e76-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="21e76-273">執行下列命令來安裝主要目標。</span><span class="sxs-lookup"><span data-stu-id="21e76-273">Run the following command to install the master target.</span></span> <span data-ttu-id="21e76-274">選擇 [Master Target]\(主要目標\) 作為代理程式角色。</span><span class="sxs-lookup"><span data-stu-id="21e76-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="21e76-275">選擇預設安裝位置，然後按 **Enter** 以繼續。</span><span class="sxs-lookup"><span data-stu-id="21e76-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![選擇主要目標的預設安裝位置](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="21e76-277">安裝完成之後，使用命令列來註冊組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="21e76-278">記下組態伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="21e76-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="21e76-279">您在下一步需要用到它。</span><span class="sxs-lookup"><span data-stu-id="21e76-279">You need it in the next step.</span></span>

2. <span data-ttu-id="21e76-280">執行下列命令來安裝主要目標伺服器，並向組態伺服器註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="21e76-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="21e76-281">範例：</span><span class="sxs-lookup"><span data-stu-id="21e76-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="21e76-282">等候指令碼完成。</span><span class="sxs-lookup"><span data-stu-id="21e76-282">Wait until the script finishes.</span></span> <span data-ttu-id="21e76-283">如果主要目標註冊成功，主要目標會列在入口網站的 [Site Recovery 基礎結構] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="21e76-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="21e76-284">升級主要目標</span><span class="sxs-lookup"><span data-stu-id="21e76-284">Upgrade the master target</span></span>

<span data-ttu-id="21e76-285">執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="21e76-285">Run the installer.</span></span> <span data-ttu-id="21e76-286">它會自動偵測主要目標上是否已安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="21e76-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="21e76-287">選取 [Y]\(是\) 進行升級。安裝完成之後，您可以使用下列命令來檢查所安裝的主要目標版本。</span><span class="sxs-lookup"><span data-stu-id="21e76-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="21e76-288">您可以看到 [VERSION]\(版本\) 欄位中提供的主要目標版本號碼。</span><span class="sxs-lookup"><span data-stu-id="21e76-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="21e76-289">在主要目標伺服器上安裝 VMware 工具</span><span class="sxs-lookup"><span data-stu-id="21e76-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="21e76-290">您必須將 VMware 工具安裝在主要目標上，以便其探索資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21e76-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="21e76-291">如果未安裝工具，重新保護畫面就不會列出資料存放區。</span><span class="sxs-lookup"><span data-stu-id="21e76-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="21e76-292">安裝 VMware 工具之後，您必須重新開機。</span><span class="sxs-lookup"><span data-stu-id="21e76-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e76-293">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21e76-293">Next steps</span></span>
<span data-ttu-id="21e76-294">在主要目標完成安裝和註冊之後，您可以看到主要目標出現在 [Site Recovery 基礎結構] 中的 [主要目標] 區段 (在組態伺服器概觀下)。</span><span class="sxs-lookup"><span data-stu-id="21e76-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="21e76-295">您現在可以繼續[重新保護](site-recovery-how-to-reprotect.md)，接著進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="21e76-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="21e76-296">常見問題</span><span class="sxs-lookup"><span data-stu-id="21e76-296">Common issues</span></span>

* <span data-ttu-id="21e76-297">請確定您未在任何管理元件 (例如主要目標) 上啟動 Storage vMotion。</span><span class="sxs-lookup"><span data-stu-id="21e76-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="21e76-298">如果在成功重新保護之後主要目標有移動，則無法中斷連結虛擬機器磁碟 (VMDK)。</span><span class="sxs-lookup"><span data-stu-id="21e76-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="21e76-299">在此情況下，容錯回復會失敗。</span><span class="sxs-lookup"><span data-stu-id="21e76-299">In this case, failback fails.</span></span>

* <span data-ttu-id="21e76-300">主要目標在虛擬機器上不應該有任何快照集。</span><span class="sxs-lookup"><span data-stu-id="21e76-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="21e76-301">如果有快照集，容錯回復會失敗。</span><span class="sxs-lookup"><span data-stu-id="21e76-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="21e76-302">由於某些客戶會有一些自訂 NIC 組態，因此啟動期間會停用網路介面，導致主要目標代理程式無法初始化。</span><span class="sxs-lookup"><span data-stu-id="21e76-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="21e76-303">請確定已正確設定下列屬性。</span><span class="sxs-lookup"><span data-stu-id="21e76-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="21e76-304">在乙太網路卡檔案的 /etc/sysconfig/network-scripts/ifcfg-eth* 中檢查這些屬性。</span><span class="sxs-lookup"><span data-stu-id="21e76-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="21e76-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="21e76-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="21e76-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="21e76-306">ONBOOT=yes</span></span>

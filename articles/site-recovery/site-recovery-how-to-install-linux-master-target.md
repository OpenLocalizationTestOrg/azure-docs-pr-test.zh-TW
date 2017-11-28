---
title: "aaaHow tooinstall 從 Azure tooon 內部部署容錯移轉的 Linux 主要目標伺服器 |Microsoft 文件"
description: "在重新保護 Linux 虛擬機器之前，您必須先有 Linux 主要目標伺服器。 深入了解如何 tooinstall 其中一個。"
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
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="a41d5-104">安裝 Linux 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="a41d5-104">Install a Linux master target server</span></span>
<span data-ttu-id="a41d5-105">您虛擬機器容錯移轉之後，您可以容錯回復 hello 虛擬機器 toohello 在內部部署站台。</span><span class="sxs-lookup"><span data-stu-id="a41d5-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="a41d5-106">toofail 上一步，您需要從 Azure toohello 在內部部署站台 tooreprotect hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="a41d5-107">此程序，您需要在內部部署主要目標伺服器 tooreceive hello 流量。</span><span class="sxs-lookup"><span data-stu-id="a41d5-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="a41d5-108">如果受保護的虛擬機器是 Windows 虛擬機器，您需要 Windows 主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="a41d5-109">若是 Linux 虛擬機器，您需要 Linux 主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="a41d5-110">讀取 hello 下列步驟 toolearn toocreate 並安裝 Linux 主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a41d5-111">從 hello 9.10.0 主要目標伺服器的版本開始，hello 最新的主要目標伺服器可以只安裝 Ubuntu 16.04 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="a41d5-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="a41d5-112">CentOS6.6 伺服器上不允許安裝新的主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="a41d5-113">不過，您可以繼續 tooupgrade 舊的主要目標伺服器使用 hello 9.10.0 版本。</span><span class="sxs-lookup"><span data-stu-id="a41d5-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="a41d5-114">概觀</span><span class="sxs-lookup"><span data-stu-id="a41d5-114">Overview</span></span>
<span data-ttu-id="a41d5-115">本文說明如何 tooinstall Linux 主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="a41d5-116">將註解或問題張貼結尾 hello 這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="a41d5-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a41d5-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="a41d5-117">Prerequisites</span></span>

* <span data-ttu-id="a41d5-118">toochoose hello 主機上的 toodeploy hello 的主要目標，判斷 toobe tooan 現有內部部署虛擬機器或 tooa 新的虛擬機器時，是否要將 hello 容錯回復。</span><span class="sxs-lookup"><span data-stu-id="a41d5-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="a41d5-119">現有的虛擬機器 hello 主要目標的 hello 主機應該具有存取 toohello 資料存放區的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="a41d5-120">如果 hello 在內部部署虛擬機器不存在，hello 相同裝載為 hello 主要目標上建立 hello 容錯回復虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="a41d5-121">您可以選擇任何 ESXi 主機 tooinstall hello 主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="a41d5-122">hello 主要目標應該是可以與 hello 處理序伺服器和 hello 組態伺服器通訊的網路上。</span><span class="sxs-lookup"><span data-stu-id="a41d5-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="a41d5-123">hello 版本 hello 主要目標必須等於 tooor 早於 hello hello 處理序伺服器和伺服器 hello 組態版本。</span><span class="sxs-lookup"><span data-stu-id="a41d5-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="a41d5-124">例如，9.4 hello 組態伺服器的 hello 版本時，hello hello 主要的目標版本可以 9.4 或 9.3 不 9.5。</span><span class="sxs-lookup"><span data-stu-id="a41d5-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="a41d5-125">hello 主要目標只能是 VMware 虛擬機器而不是實體的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="a41d5-126">建立 hello 主要的目標，根據 toohello 調整大小的指導方針</span><span class="sxs-lookup"><span data-stu-id="a41d5-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="a41d5-127">建立根據調整大小的指導方針的 hello hello 主要目標：</span><span class="sxs-lookup"><span data-stu-id="a41d5-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="a41d5-128">**RAM**：6 GB 或更多</span><span class="sxs-lookup"><span data-stu-id="a41d5-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="a41d5-129">**作業系統磁碟大小**: 100 GB 或更多的 (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="a41d5-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="a41d5-130">**用於保留磁碟機的額外磁碟大小**：1 TB</span><span class="sxs-lookup"><span data-stu-id="a41d5-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="a41d5-131">**CPU 核心**：4 核心或更多</span><span class="sxs-lookup"><span data-stu-id="a41d5-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="a41d5-132">hello 下列支援的 Ubuntu 支援核心。</span><span class="sxs-lookup"><span data-stu-id="a41d5-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="a41d5-133">核心系列</span><span class="sxs-lookup"><span data-stu-id="a41d5-133">Kernel Series</span></span>  |<span data-ttu-id="a41d5-134">支援註冊太</span><span class="sxs-lookup"><span data-stu-id="a41d5-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="a41d5-135">4.4</span><span class="sxs-lookup"><span data-stu-id="a41d5-135">4.4</span></span>      |<span data-ttu-id="a41d5-136">4.4.0-81-generic</span><span class="sxs-lookup"><span data-stu-id="a41d5-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="a41d5-137">4.8</span><span class="sxs-lookup"><span data-stu-id="a41d5-137">4.8</span></span>      |<span data-ttu-id="a41d5-138">4.8.0-56-generic</span><span class="sxs-lookup"><span data-stu-id="a41d5-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="a41d5-139">4.10</span><span class="sxs-lookup"><span data-stu-id="a41d5-139">4.10</span></span>     |<span data-ttu-id="a41d5-140">4.10.0-24-generic</span><span class="sxs-lookup"><span data-stu-id="a41d5-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="a41d5-141">部署 hello 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="a41d5-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="a41d5-142">安裝 Ubuntu 16.04.2 極簡版</span><span class="sxs-lookup"><span data-stu-id="a41d5-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="a41d5-143">需要 hello 遵循 hello 步驟 tooinstall hello Ubuntu 16.04.2 64 位元作業系統。</span><span class="sxs-lookup"><span data-stu-id="a41d5-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="a41d5-144">**步驟 1:**移 toohello[下載連結](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64)選擇 hello 最接近鏡像從其下載 Ubuntu 16.04.2 最小 64 位元 ISO。</span><span class="sxs-lookup"><span data-stu-id="a41d5-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="a41d5-145">保留最小 64 位元 ISO Ubuntu 16.04.2 hello DVD 光碟機中並啟動 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="a41d5-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="a41d5-146">**步驟2：**選取 [English]\(英文\) 作為慣用語言，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![選取語言](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="a41d5-148">**步驟 3：**選取 [Install Ubuntu Server]\(安裝 Ubuntu 伺服器\)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![選取安裝 Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="a41d5-150">**步驟 4：**選取 [English]\(英文\) 作為慣用語言，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![選取 English 作為慣用語言](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="a41d5-152">**步驟 5:**選取 hello 適當的選項，從 hello**時區**選項清單，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![選取 hello 正確設定的時區](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="a41d5-154">**步驟 6:**選取**否**(hello 預設選項)，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Hello 鍵盤設定](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="a41d5-156">**步驟 7:**選取**英文 （美國）**為 hello 國家的 hello 鍵盤的來源，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![選取 hello 國家/地區為美國](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="a41d5-158">**步驟 8:**選取**英文 （美國）**作為 hello 鍵盤配置，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![做為 hello 鍵盤配置中選取 英文 （美國）](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="a41d5-160">**步驟 9:**輸入您的伺服器 hello hello 主機名稱**Hostname**方塊，並選取**繼續**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![輸入您的伺服器 hello 主機名稱](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="a41d5-162">**步驟 10:** toocreate 使用者帳戶，輸入 hello 使用者名稱，然後選取**繼續**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![建立使用者帳戶](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="a41d5-164">**步驟 11:** hello 新的使用者帳戶，請輸入 hello 密碼，然後選取**繼續**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![輸入 hello 密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="a41d5-166">**步驟 12:**確認 hello hello 新使用者的密碼，然後選取 **繼續**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![確認 hello 密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="a41d5-168">**步驟 13:**選取**否**(hello 預設選項)，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![設定使用者和密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="a41d5-170">**步驟 14:**顯示 hello 時區是正確的如果選取**是**(hello 預設選項)，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="a41d5-171">tooreconfigure 您的時區，選取**否**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-171">tooreconfigure your time zone, select **No**.</span></span>

![設定 hello 時鐘](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="a41d5-173">**步驟 15:** hello 分割方式選項，從選取**指引-使用完整磁碟**，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![選取資料分割方法選項 hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="a41d5-175">**步驟 16:**選取 hello 適當的磁碟與 hello**選取磁碟 toopartition**選項，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![選取 hello 磁碟](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="a41d5-177">**步驟 17:**選取**是**toowrite hello 變更 toodisk，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![寫入 hello 變更 toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="a41d5-179">**步驟 18:**選取 hello 預設選項，請選取**繼續**，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![選取 hello 預設選項](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="a41d5-181">**步驟 19:**選取 hello 適當的選項，來管理您的系統上的升級，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![選取 toomanage 如何升級](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="a41d5-183">Hello Azure Site Recovery 的主要目標伺服器需要非常特定的 hello Ubuntu 版本，因此您需要 tooensure 升級已停用該 hello 核心 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="a41d5-184">如果有啟用，任何規則的升級會造成 hello 主要目標伺服器 toomalfunction。</span><span class="sxs-lookup"><span data-stu-id="a41d5-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="a41d5-185">請確定您選取 hello**沒有自動更新**選項。</span><span class="sxs-lookup"><span data-stu-id="a41d5-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="a41d5-186">**步驟 20：**選取預設選項。</span><span class="sxs-lookup"><span data-stu-id="a41d5-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="a41d5-187">如果您想 openSSH，SSH 連線，請選取 hello **OpenSSH 伺服器**選項，然後再選取**繼續**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![選取軟體](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="a41d5-189">**步驟 21：**選取 [Yes](是\)，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![安裝 hello 幼蟲開機載入器](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="a41d5-191">**步驟 22:**選取 hello hello 開機載入器安裝適當的裝置 (最好是**/開發/sda**)，然後選取**Enter**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![選取裝置以安裝開機載入器](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="a41d5-193">**步驟 23:**選取**繼續**，然後選取**Enter** toofinish hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="a41d5-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![完成 hello 安裝](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="a41d5-195">Hello 安裝完成之後，登入 toohello VM 與 hello 新的使用者認證。</span><span class="sxs-lookup"><span data-stu-id="a41d5-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="a41d5-196">(請參閱太**步驟 10**如需詳細資訊。)</span><span class="sxs-lookup"><span data-stu-id="a41d5-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="a41d5-197">採取 hello 步驟所述的下列螢幕擷取畫面 tooset hello 根 hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="a41d5-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="a41d5-198">然後以根使用者的身分登入。</span><span class="sxs-lookup"><span data-stu-id="a41d5-198">Then sign in as ROOT user.</span></span>

![設定 hello 根使用者密碼](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="a41d5-200">做為主要目標伺服器準備 hello 機器組態</span><span class="sxs-lookup"><span data-stu-id="a41d5-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="a41d5-201">接下來，做為主要目標伺服器準備 hello 機器組態。</span><span class="sxs-lookup"><span data-stu-id="a41d5-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="a41d5-202">在 Linux 虛擬機器中，每個 SCSI 磁碟 tooget hello 識別碼啟用 hello**磁碟。EnableUUID = TRUE**參數。</span><span class="sxs-lookup"><span data-stu-id="a41d5-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="a41d5-203">tooenable 這個參數，採用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a41d5-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="a41d5-204">關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="a41d5-205">Hello hello hello 左窗格中的虛擬機器的項目上按一下滑鼠右鍵，然後選取**編輯設定**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="a41d5-206">選取 hello**選項** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a41d5-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="a41d5-207">Hello 左窗格中，選取**進階** > **一般**，然後選取 hello**組態參數**hello 右下方的組件的囉 」 畫面上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a41d5-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![[選項] 索引標籤](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="a41d5-209">hello**組態參數**hello 機器執行時，並非可使用選項。</span><span class="sxs-lookup"><span data-stu-id="a41d5-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="a41d5-210">toomake 作用中，此索引標籤的 hello 虛擬機器關機。</span><span class="sxs-lookup"><span data-stu-id="a41d5-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="a41d5-211">查看含有 [disk.EnableUUID] 的資料列是否已經存在。</span><span class="sxs-lookup"><span data-stu-id="a41d5-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="a41d5-212">如果 hello 值存在而且設定得**False**，也變更 hello 值**True**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="a41d5-213">（hello 值是不區分大小寫）。</span><span class="sxs-lookup"><span data-stu-id="a41d5-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="a41d5-214">如果 hello 值存在而且設定得**True**，選取**取消**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="a41d5-215">如果 hello 值不存在，請選取**加入資料列**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="a41d5-216">在 hello 名稱 欄位加入**磁碟。EnableUUID**，然後將 hello 值設定太**TRUE**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![檢查 disk.EnableUUID 是否已存在](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="a41d5-218">停用核心升級</span><span class="sxs-lookup"><span data-stu-id="a41d5-218">Disable kernel upgrades</span></span>

<span data-ttu-id="a41d5-219">Azure Site Recovery 的主要目標伺服器需要非常特定的 hello Ubuntu 版本，請確定 hello 核心升級已停用 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="a41d5-220">如果已啟用核心升級，任何規則的升級會造成 hello 主要目標伺服器 toomalfunction。</span><span class="sxs-lookup"><span data-stu-id="a41d5-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="a41d5-221">下載並安裝其他套件</span><span class="sxs-lookup"><span data-stu-id="a41d5-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="a41d5-222">請確定您有網際網路連線 toodownload，並安裝其他的封裝。</span><span class="sxs-lookup"><span data-stu-id="a41d5-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="a41d5-223">如果您沒有網際網路連線，您需要 toomanually 尋找這些 RPM 套件並安裝它們。</span><span class="sxs-lookup"><span data-stu-id="a41d5-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="a41d5-224">取得安裝程式中的 hello 安裝程式</span><span class="sxs-lookup"><span data-stu-id="a41d5-224">Get hello installer for setup</span></span>

<span data-ttu-id="a41d5-225">如果您的主要目標有網際網路連線，您可以使用下列步驟 toodownload hello installer hello。</span><span class="sxs-lookup"><span data-stu-id="a41d5-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="a41d5-226">或者，您可以複製 hello installer 從 hello 處理序伺服器，然後再安裝它。</span><span class="sxs-lookup"><span data-stu-id="a41d5-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="a41d5-227">下載 hello 主要目標安裝封裝</span><span class="sxs-lookup"><span data-stu-id="a41d5-227">Download hello master target installation packages</span></span>

<span data-ttu-id="a41d5-228">[下載 hello 最新 Linux 主要目標安裝 bits](https://aka.ms/latestlinuxmobsvc)。</span><span class="sxs-lookup"><span data-stu-id="a41d5-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="a41d5-229">toodownload 它使用 Linux，類型：</span><span class="sxs-lookup"><span data-stu-id="a41d5-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="a41d5-230">請確定您下載並解壓縮您的主目錄中的 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a41d5-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="a41d5-231">如果您將解壓縮太**/usr/本機**，則 hello 安裝會失敗。</span><span class="sxs-lookup"><span data-stu-id="a41d5-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="a41d5-232">從 hello 處理序伺服器存取 hello 安裝程式</span><span class="sxs-lookup"><span data-stu-id="a41d5-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="a41d5-233">Hello 程序在伺服器上，前往 太**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="a41d5-234">將 hello 必要的安裝程式檔案複製從 hello 處理序伺服器，並將它儲存成**latestlinuxmobsvc.tar.gz**主目錄中。</span><span class="sxs-lookup"><span data-stu-id="a41d5-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="a41d5-235">套用自訂組態變更</span><span class="sxs-lookup"><span data-stu-id="a41d5-235">Apply custom configuration changes</span></span>

<span data-ttu-id="a41d5-236">下列步驟使用 hello tooapply 自訂組態變更：</span><span class="sxs-lookup"><span data-stu-id="a41d5-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="a41d5-237">執行下列命令 toountar hello 二進位 hello。</span><span class="sxs-lookup"><span data-stu-id="a41d5-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Hello 命令 toorun 的螢幕擷取畫面](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="a41d5-239">執行下列命令 toogive 權限的 hello。</span><span class="sxs-lookup"><span data-stu-id="a41d5-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="a41d5-240">執行下列命令 toorun hello 指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="a41d5-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="a41d5-241">Hello 伺服器上執行一次 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a41d5-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="a41d5-242">關閉 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-242">Shut down hello server.</span></span> <span data-ttu-id="a41d5-243">然後重新啟動伺服器 hello 之後新增磁碟，hello 下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="a41d5-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="a41d5-244">加入保留磁碟 toohello Linux 主要目標虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a41d5-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="a41d5-245">使用下列步驟 toocreate 保留磁碟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a41d5-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="a41d5-246">附加新 1 TB 磁碟 toohello Linux 主要目標虛擬機器，然後再啟動 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="a41d5-247">使用 hello**多重路徑 ll**命令 toolearn hello 多重路徑磁碟的識別碼 hello 保留。</span><span class="sxs-lookup"><span data-stu-id="a41d5-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![hello hello 保留磁碟多重路徑識別碼](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="a41d5-249">格式化 hello 磁碟機，並再建立 hello 新磁碟機上的 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="a41d5-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Hello 磁碟機上建立檔案系統](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="a41d5-251">建立 hello 檔案系統之後，掛接 hello 保留磁碟。</span><span class="sxs-lookup"><span data-stu-id="a41d5-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![掛接 hello 保留磁碟](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="a41d5-253">建立 hello **fstab**項目 toomount hello 保留磁碟機每次 hello 系統啟動時啟動。</span><span class="sxs-lookup"><span data-stu-id="a41d5-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="a41d5-254">選取**插入**toobegin 編輯 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a41d5-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="a41d5-255">建立新的一行，然後再 hello 文字之後。</span><span class="sxs-lookup"><span data-stu-id="a41d5-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="a41d5-256">編輯 hello 磁碟多重路徑識別碼根據 hello 反白顯示 hello 前一個命令從多重路徑的識別碼。</span><span class="sxs-lookup"><span data-stu-id="a41d5-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="a41d5-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="a41d5-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="a41d5-258">選取**Esc**，然後輸入**: wq** （寫入及結束） tooclose hello 編輯器 視窗。</span><span class="sxs-lookup"><span data-stu-id="a41d5-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="a41d5-259">安裝主要目標的 hello</span><span class="sxs-lookup"><span data-stu-id="a41d5-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a41d5-260">hello hello 主要目標伺服器版本必須等於 tooor 早於 hello 版本 hello 處理序伺服器和伺服器 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="a41d5-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="a41d5-261">如果不符合此條件，重新保護會成功，但複寫會失敗。</span><span class="sxs-lookup"><span data-stu-id="a41d5-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="a41d5-262">安裝 hello 主要目標伺服器之前，請檢查該 hello **/etc/hosts 主機**hello 虛擬機器上的檔案包含對應 hello 本機主機名稱 toohello IP 位址與所有網路介面卡相關聯的項目。</span><span class="sxs-lookup"><span data-stu-id="a41d5-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="a41d5-263">複製 hello 複雜密碼**C:\ProgramData\Microsoft Azure 站台 Recovery\private\connection.passphrase** hello 組態伺服器上。</span><span class="sxs-lookup"><span data-stu-id="a41d5-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="a41d5-264">然後將它儲存成**passphrase.txt** hello 中執行相同的本機目錄 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="a41d5-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="a41d5-265">範例：</span><span class="sxs-lookup"><span data-stu-id="a41d5-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="a41d5-266">請注意 hello 組態伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a41d5-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="a41d5-267">您需要在 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a41d5-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="a41d5-268">執行下列命令 tooinstall hello 主要目標伺服器 hello 和伺服器 hello hello 組態伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="a41d5-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="a41d5-269">範例：</span><span class="sxs-lookup"><span data-stu-id="a41d5-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="a41d5-270">等候 hello 指令碼完成。</span><span class="sxs-lookup"><span data-stu-id="a41d5-270">Wait until hello script finishes.</span></span> <span data-ttu-id="a41d5-271">如果主要目標的 hello 註冊成功，hello 主要目標列在 hello **Site Recovery 基礎結構**hello 入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="a41d5-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="a41d5-272">使用互動式安裝來安裝 hello 主要目標</span><span class="sxs-lookup"><span data-stu-id="a41d5-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="a41d5-273">執行下列命令 tooinstall hello 主要目標的 hello。</span><span class="sxs-lookup"><span data-stu-id="a41d5-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="a41d5-274">對於 hello 代理程式角色，請選擇**主要目標**。</span><span class="sxs-lookup"><span data-stu-id="a41d5-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="a41d5-275">選擇 hello 預設安裝位置，然後選取**Enter** toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a41d5-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![選擇主要目標的預設安裝位置](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="a41d5-277">Hello 安裝完成之後，請使用 hello 命令列註冊 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="a41d5-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="a41d5-278">請注意 hello hello 組態伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a41d5-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="a41d5-279">您需要在 hello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a41d5-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="a41d5-280">執行下列命令 tooinstall hello 主要目標伺服器 hello 和伺服器 hello hello 組態伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="a41d5-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="a41d5-281">範例：</span><span class="sxs-lookup"><span data-stu-id="a41d5-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="a41d5-282">等候 hello 指令碼完成。</span><span class="sxs-lookup"><span data-stu-id="a41d5-282">Wait until hello script finishes.</span></span> <span data-ttu-id="a41d5-283">如果 hello 主要目標是已登錄的成功，hello 主要目標列在 hello **Site Recovery 基礎結構**hello 入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="a41d5-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="a41d5-284">升級 hello 主要目標</span><span class="sxs-lookup"><span data-stu-id="a41d5-284">Upgrade hello master target</span></span>

<span data-ttu-id="a41d5-285">執行 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a41d5-285">Run hello installer.</span></span> <span data-ttu-id="a41d5-286">它會自動偵測 hello 主要目標上安裝該 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="a41d5-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="a41d5-287">選取 tooupgrade **Y**。Hello 安裝完成之後，請檢查 hello 版本 hello 使用 hello 下列命令來安裝的主要目標。</span><span class="sxs-lookup"><span data-stu-id="a41d5-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="a41d5-288">您可以看到該 hello**版本**欄位提供的 hello 主要目標的 hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="a41d5-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="a41d5-289">Hello 主要目標伺服器上安裝 VMware 工具</span><span class="sxs-lookup"><span data-stu-id="a41d5-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="a41d5-290">您需要 tooinstall hello 主要目標上的 VMware 工具，讓它可以找出 hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a41d5-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="a41d5-291">如果未安裝 hello 工具，重新保護囉 」 畫面未列在 hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a41d5-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="a41d5-292">安裝之後 hello VMware 工具，您需要 toorestart。</span><span class="sxs-lookup"><span data-stu-id="a41d5-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a41d5-293">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a41d5-293">Next steps</span></span>
<span data-ttu-id="a41d5-294">Hello 安裝和註冊 hello 主要目標有 finsihed 之後，您可以查看 hello 主要目標出現在 hello**主要目標**一節中**Site Recovery 基礎結構**，底下 hello設定伺服器的概觀。</span><span class="sxs-lookup"><span data-stu-id="a41d5-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="a41d5-295">您現在可以繼續[重新保護](site-recovery-how-to-reprotect.md)，接著進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="a41d5-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="a41d5-296">常見問題</span><span class="sxs-lookup"><span data-stu-id="a41d5-296">Common issues</span></span>

* <span data-ttu-id="a41d5-297">請確定您未在任何管理元件 (例如主要目標) 上啟動 Storage vMotion。</span><span class="sxs-lookup"><span data-stu-id="a41d5-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="a41d5-298">如果 hello 主要目標移動成功的重新保護之後，就無法卸離 hello 虛擬機器磁碟 (Vmdk)。</span><span class="sxs-lookup"><span data-stu-id="a41d5-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="a41d5-299">在此情況下，容錯回復會失敗。</span><span class="sxs-lookup"><span data-stu-id="a41d5-299">In this case, failback fails.</span></span>

* <span data-ttu-id="a41d5-300">hello 主要目標不應該有 hello 虛擬機器上的任何快照集。</span><span class="sxs-lookup"><span data-stu-id="a41d5-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="a41d5-301">如果有快照集，容錯回復會失敗。</span><span class="sxs-lookup"><span data-stu-id="a41d5-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="a41d5-302">由於 toosome 自訂 NIC 上設定某些客戶，hello 網路介面已停用在啟動期間，與 hello 主要目標代理程式無法初始化。</span><span class="sxs-lookup"><span data-stu-id="a41d5-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="a41d5-303">請確定已正確設定下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="a41d5-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="a41d5-304">請檢查這些屬性在 hello 乙太網路介面卡檔案的 /etc/sysconfig/network-scripts/ifcfg-eth *。</span><span class="sxs-lookup"><span data-stu-id="a41d5-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="a41d5-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="a41d5-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="a41d5-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="a41d5-306">ONBOOT=yes</span></span>

---
title: "Azure Site Recovery 的複寫設定 aaaSet |Microsoft 文件"
description: "描述如何 toodeploy Site Recovery tooorchestrate 複寫、 容錯移轉和復原 VMM 中的 HYPER-V Vm 的雲端 tooAzure。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="1cff1-103">管理 VMware tooAzure 的複寫的原則</span><span class="sxs-lookup"><span data-stu-id="1cff1-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="1cff1-104">建立複寫原則</span><span class="sxs-lookup"><span data-stu-id="1cff1-104">Create a replication policy</span></span>

1. <span data-ttu-id="1cff1-105">選取 [管理] > [Site Recovery 基礎結構]。</span><span class="sxs-lookup"><span data-stu-id="1cff1-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="1cff1-106">在 [VMware 和實體機器] 下選取 [複寫原則]。</span><span class="sxs-lookup"><span data-stu-id="1cff1-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="1cff1-107">選取 [+複寫原則]。</span><span class="sxs-lookup"><span data-stu-id="1cff1-107">Select **+Replication policy**.</span></span>

    ![建立複寫原則](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="1cff1-109">輸入 hello 原則名稱。</span><span class="sxs-lookup"><span data-stu-id="1cff1-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="1cff1-110">在**RPO 臨界值**，指定 hello RPO 上限。</span><span class="sxs-lookup"><span data-stu-id="1cff1-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="1cff1-111">連續複寫超過此限制時，會產生警示。</span><span class="sxs-lookup"><span data-stu-id="1cff1-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="1cff1-112">在**復原點保留**，指定 （以小時為單位） hello hello 保留期間的每個復原點的持續時間。</span><span class="sxs-lookup"><span data-stu-id="1cff1-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="1cff1-113">受保護的電腦可以是復原 tooany 點內的保留週期。</span><span class="sxs-lookup"><span data-stu-id="1cff1-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1cff1-114">Too24 小時保留的總機器複寫的 toopremium 存放裝置的支援。</span><span class="sxs-lookup"><span data-stu-id="1cff1-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="1cff1-115">Too72 小時保留的總機器複寫的 toostandard 存放裝置的支援。</span><span class="sxs-lookup"><span data-stu-id="1cff1-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1cff1-116">系統會自動建立容錯回復的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="1cff1-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="1cff1-117">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="1cff1-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="1cff1-118">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1cff1-118">Click **OK**.</span></span> <span data-ttu-id="1cff1-119">應該在 30 too60 秒內建立 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="1cff1-119">hello policy should be created in 30 too60 seconds.</span></span>

![產生複寫原則](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="1cff1-121">使組態伺服器與複寫原則產生關聯</span><span class="sxs-lookup"><span data-stu-id="1cff1-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="1cff1-122">選擇 hello 複寫原則 toowhich 想 tooassociate hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cff1-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="1cff1-123">按一下 [關聯]。</span><span class="sxs-lookup"><span data-stu-id="1cff1-123">Click **Associate**.</span></span>
<span data-ttu-id="1cff1-124">![關聯組態伺服器](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="1cff1-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="1cff1-125">從伺服器 hello 清單中選取 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cff1-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="1cff1-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1cff1-126">Click **OK**.</span></span> <span data-ttu-id="1cff1-127">hello 組態伺服器應該與其相關以一個 tootwo 分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="1cff1-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![關聯組態伺服器](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="1cff1-129">編輯複寫原則</span><span class="sxs-lookup"><span data-stu-id="1cff1-129">Edit a replication policy</span></span>
1. <span data-ttu-id="1cff1-130">選擇您想要的 tooedit 複寫設定的 hello 複寫原則。</span><span class="sxs-lookup"><span data-stu-id="1cff1-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="1cff1-131">![編輯複寫原則](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="1cff1-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="1cff1-132">按一下 [編輯設定] 。</span><span class="sxs-lookup"><span data-stu-id="1cff1-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="1cff1-133">![編輯複寫原則設定](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="1cff1-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="1cff1-134">變更您的需求為基礎的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="1cff1-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="1cff1-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1cff1-135">Click **Save**.</span></span> <span data-ttu-id="1cff1-136">hello 原則應該儲存在兩個 toofive 分鐘，視多少 Vm 會使用該複寫原則。</span><span class="sxs-lookup"><span data-stu-id="1cff1-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![儲存複寫原則](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="1cff1-138">使組態伺服器與複寫原則中斷關聯</span><span class="sxs-lookup"><span data-stu-id="1cff1-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="1cff1-139">選擇 hello 複寫原則 toowhich 想 tooassociate hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cff1-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="1cff1-140">按一下 [中斷關聯]。</span><span class="sxs-lookup"><span data-stu-id="1cff1-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="1cff1-141">從伺服器 hello 清單中選取 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cff1-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="1cff1-142">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1cff1-142">Click **OK**.</span></span> <span data-ttu-id="1cff1-143">hello 組態伺服器應該取消關聯，以一個 tootwo 分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="1cff1-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1cff1-144">如果沒有至少一個複寫的項目使用 hello 原則，無法中斷與組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cff1-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="1cff1-145">請確定沒有使用 hello 原則之前中斷與 hello 組態伺服器的複寫項目。</span><span class="sxs-lookup"><span data-stu-id="1cff1-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="1cff1-146">刪除複寫原則</span><span class="sxs-lookup"><span data-stu-id="1cff1-146">Delete a replication policy</span></span>

1. <span data-ttu-id="1cff1-147">選擇 hello 複寫原則的 toodelete。</span><span class="sxs-lookup"><span data-stu-id="1cff1-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="1cff1-148">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="1cff1-148">Click **Delete**.</span></span> <span data-ttu-id="1cff1-149">hello 原則應該刪除 30 too60 （秒）。</span><span class="sxs-lookup"><span data-stu-id="1cff1-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1cff1-150">如果有至少一個組態相關聯伺服器 tooit，您無法刪除的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="1cff1-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="1cff1-151">請確定沒有任何複寫的項目，使用 hello 原則並刪除 hello 原則之前，先刪除所有 hello 相關聯設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="1cff1-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>

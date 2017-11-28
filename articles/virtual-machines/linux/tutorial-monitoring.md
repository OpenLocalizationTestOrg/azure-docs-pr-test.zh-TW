---
title: "在 Azure 中的 aaaMonitor Linux 虛擬機器 |Microsoft 文件"
description: "了解如何 toomonitor 開機診斷和效能度量資訊在 Azure 中 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="a3df1-103">如何在 Azure 中 Linux 虛擬機器 toomonitor</span><span class="sxs-lookup"><span data-stu-id="a3df1-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="a3df1-104">tooensure 您在 Azure 中的虛擬機器 (Vm) 正常運作，您可以檢閱開機診斷和效能度量。</span><span class="sxs-lookup"><span data-stu-id="a3df1-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="a3df1-105">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="a3df1-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3df1-106">啟用 hello VM 上的開機診斷功能</span><span class="sxs-lookup"><span data-stu-id="a3df1-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="a3df1-107">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="a3df1-107">View boot diagnostics</span></span>
> * <span data-ttu-id="a3df1-108">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="a3df1-108">View host metrics</span></span>
> * <span data-ttu-id="a3df1-109">啟用 hello VM 的診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="a3df1-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="a3df1-110">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="a3df1-110">View VM metrics</span></span>
> * <span data-ttu-id="a3df1-111">依據診斷計量建立警示</span><span class="sxs-lookup"><span data-stu-id="a3df1-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="a3df1-112">設定進階監視</span><span class="sxs-lookup"><span data-stu-id="a3df1-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a3df1-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="a3df1-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a3df1-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="a3df1-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a3df1-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a3df1-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="a3df1-116">建立 VM</span><span class="sxs-lookup"><span data-stu-id="a3df1-116">Create VM</span></span>

<span data-ttu-id="a3df1-117">toosee 診斷和動作中的度量，您需要在 VM。</span><span class="sxs-lookup"><span data-stu-id="a3df1-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="a3df1-118">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="a3df1-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a3df1-119">hello 下列範例會建立名為的資源群組*myResourceGroupMonitor*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="a3df1-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="a3df1-120">現在，使用 [az vm create](https://docs.microsoft.com/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="a3df1-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="a3df1-121">hello 下列範例會建立名為的 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="a3df1-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="a3df1-122">啟用開機診斷</span><span class="sxs-lookup"><span data-stu-id="a3df1-122">Enable boot diagnostics</span></span>

<span data-ttu-id="a3df1-123">Linux Vm 開機，因為 hello 開機診斷延伸模組會擷取開機輸出，並將它儲存在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3df1-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="a3df1-124">此資料可以使用的 tootroubleshoot VM 開機問題。</span><span class="sxs-lookup"><span data-stu-id="a3df1-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="a3df1-125">當您建立使用 Azure CLI hello 的 Linux VM 時，不會自動啟用開機診斷。</span><span class="sxs-lookup"><span data-stu-id="a3df1-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="a3df1-126">之前啟用開機診斷功能，必須 toobe 儲存開機記錄檔中建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3df1-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="a3df1-127">儲存體帳戶必須具有全域唯一的名稱，介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="a3df1-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="a3df1-128">建立儲存體帳戶以 hello [az 儲存體帳戶建立](/cli/azure/storage/account#create)命令。</span><span class="sxs-lookup"><span data-stu-id="a3df1-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="a3df1-129">在此範例中，隨機字串是使用的 toocreate 獨特的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="a3df1-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="a3df1-130">當啟用開機診斷功能，則需要 hello URI toohello blob 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="a3df1-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="a3df1-131">hello 下列命令查詢 hello 儲存體帳戶 tooreturn 此 URI。</span><span class="sxs-lookup"><span data-stu-id="a3df1-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="a3df1-132">hello URI 值會儲存在變數名稱*bloburi*，hello 下一個步驟中所用。</span><span class="sxs-lookup"><span data-stu-id="a3df1-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="a3df1-133">現在，使用 [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable) 啟用開機診斷。</span><span class="sxs-lookup"><span data-stu-id="a3df1-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="a3df1-134">hello`--storage`值為 hello blob URI 收集 hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a3df1-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="a3df1-135">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="a3df1-135">View boot diagnostics</span></span>

<span data-ttu-id="a3df1-136">當啟用開機診斷時，每次您停止並啟動 VM，hello hello 開機程序的相關資訊會寫入 tooa 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a3df1-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="a3df1-137">此範例中，針對第一次解除配置 hello VM 以 hello [az vm 解除配置](/cli/azure/vm#deallocate)命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3df1-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="a3df1-138">現在開始 hello VM 以 hello [az vm 啟動]( /cli/azure/vm#stop)命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3df1-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="a3df1-139">您可以取得 hello 開機診斷資料的*myVM*以 hello [az vm 開機診斷 get 開機-記錄](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log)命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3df1-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="a3df1-140">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="a3df1-140">View host metrics</span></span>

<span data-ttu-id="a3df1-141">在 Azure 中有 Linux VM 專用的主機與它互動。</span><span class="sxs-lookup"><span data-stu-id="a3df1-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="a3df1-142">度量資訊會自動收集 hello 主機，而且可以檢視 hello Azure 入口網站中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3df1-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="a3df1-143">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroupMonitor**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="a3df1-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="a3df1-144">toosee 如何 hello 主機 VM 正在執行中，按一下**度量**hello VM 刀鋒視窗，然後選取任何 hello *[主機]*下的度量**可用的度量**。</span><span class="sxs-lookup"><span data-stu-id="a3df1-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![檢視主機計量](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="a3df1-146">安裝診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="a3df1-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3df1-147">本文件說明 2.3 版 hello Linux 診斷延伸，其中已被取代。</span><span class="sxs-lookup"><span data-stu-id="a3df1-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="a3df1-148">至 2018 年 6 月 30 日止就不再支援 2.3 版。</span><span class="sxs-lookup"><span data-stu-id="a3df1-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="a3df1-149">3.0 版的 hello Linux 診斷延伸模組可以改為啟用。</span><span class="sxs-lookup"><span data-stu-id="a3df1-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="a3df1-150">如需詳細資訊，請參閱[hello 文件](./diagnostic-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="a3df1-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="a3df1-151">hello 基本主機計量可供使用，但更細微的 toosee 和特定 VM 的度量，您 tooneed tooinstall hello Azure 診斷擴充功能在 hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="a3df1-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="a3df1-152">hello Azure 診斷擴充功能可讓其他監視和診斷資料 toobe hello VM 從擷取。</span><span class="sxs-lookup"><span data-stu-id="a3df1-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="a3df1-153">您可以檢視這些效能度量，並依據 hello VM 執行的方式建立警示。</span><span class="sxs-lookup"><span data-stu-id="a3df1-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="a3df1-154">hello 診斷延伸模組會安裝透過 hello Azure 入口網站，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a3df1-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="a3df1-155">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="a3df1-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="a3df1-156">按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="a3df1-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="a3df1-157">hello 清單顯示*開機診斷*已經啟用 hello 前一節。</span><span class="sxs-lookup"><span data-stu-id="a3df1-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="a3df1-158">按一下核取方塊 hello*基本度量*。</span><span class="sxs-lookup"><span data-stu-id="a3df1-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="a3df1-159">在 hello*儲存體帳戶*區段中，瀏覽 tooand 選取 hello *mydiagdata [1234]* hello 前一節中所建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3df1-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="a3df1-160">按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3df1-160">Click hello **Save** button.</span></span>

    ![檢視診斷計量](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="a3df1-162">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="a3df1-162">View VM metrics</span></span>

<span data-ttu-id="a3df1-163">您可以在 hello 檢視 hello VM 度量您檢視 hello 主機 VM 計量的相同方式：</span><span class="sxs-lookup"><span data-stu-id="a3df1-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="a3df1-164">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="a3df1-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="a3df1-165">toosee 如何 hello VM 正在執行中，按一下**度量**hello VM 刀鋒視窗中，且然後選取其中一個下 hello 診斷度量**可用的度量**。</span><span class="sxs-lookup"><span data-stu-id="a3df1-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![檢視 VM 計量](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="a3df1-167">建立警示</span><span class="sxs-lookup"><span data-stu-id="a3df1-167">Create alerts</span></span>

<span data-ttu-id="a3df1-168">您可以根據特定效能計量來建立警示。</span><span class="sxs-lookup"><span data-stu-id="a3df1-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="a3df1-169">警示可能會使用的 toonotify 時的平均 CPU 使用率超過某個臨界值或可用的磁碟空間低於特定大小，例如。</span><span class="sxs-lookup"><span data-stu-id="a3df1-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="a3df1-170">警示會顯示在 hello Azure 入口網站，或可以透過電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="a3df1-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="a3df1-171">您也可以在所產生的回應 tooalerts 觸發 Azure 自動化 runbook 或 Azure 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3df1-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="a3df1-172">hello 下列範例會建立警示的平均 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="a3df1-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="a3df1-173">在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。</span><span class="sxs-lookup"><span data-stu-id="a3df1-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="a3df1-174">按一下**警示規則**hello VM 刀鋒視窗，然後按一下**新增度量的警示**hello 的 hello 警示 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="a3df1-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="a3df1-175">提供警示的 [名稱]，例如 myAlertRule。</span><span class="sxs-lookup"><span data-stu-id="a3df1-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="a3df1-176">tootrigger 警示時的 CPU 百分比超過五分鐘，1.0 會保留所有 hello 選取其他預設值。</span><span class="sxs-lookup"><span data-stu-id="a3df1-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="a3df1-177">（選擇性） 核取方塊 hello*電子郵件擁有者、 參與者與讀者*toosend 電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="a3df1-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="a3df1-178">hello 預設動作是 toopresent hello 入口網站中的通知。</span><span class="sxs-lookup"><span data-stu-id="a3df1-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="a3df1-179">按一下 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a3df1-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="a3df1-180">進階監視</span><span class="sxs-lookup"><span data-stu-id="a3df1-180">Advanced monitoring</span></span> 

<span data-ttu-id="a3df1-181">您可以使用 [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) (OMS) 對您的 VM 進行更進階的監視。</span><span class="sxs-lookup"><span data-stu-id="a3df1-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="a3df1-182">如果您尚未這麼做，可以註冊 Operations Management Suite 的[免費試用版](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。</span><span class="sxs-lookup"><span data-stu-id="a3df1-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="a3df1-183">當您擁有存取 toohello OMS 入口網站時，您可以在 hello 設定 刀鋒視窗上找到 hello 工作區的索引鍵和工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="a3df1-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="a3df1-184">取代 < 工作區金鑰 > 和 < 工作區識別碼 > hello 值從您的 OMS 工作區，然後您可以使用**az vm 延伸模組集**tooadd hello OMS 擴充 toohello VM:</span><span class="sxs-lookup"><span data-stu-id="a3df1-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="a3df1-185">在 hello 記錄搜尋刀鋒視窗中的 hello OMS 入口網站，您應該看到*myVM*例如 hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="a3df1-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![OMS 刀鋒視窗](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="a3df1-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3df1-187">Next steps</span></span>

<span data-ttu-id="a3df1-188">在本教學課程中，您利用 Azure 資訊安全中心設定並檢閱 VM。</span><span class="sxs-lookup"><span data-stu-id="a3df1-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="a3df1-189">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="a3df1-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3df1-190">啟用 hello VM 上的開機診斷功能</span><span class="sxs-lookup"><span data-stu-id="a3df1-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="a3df1-191">檢視開機診斷</span><span class="sxs-lookup"><span data-stu-id="a3df1-191">View boot diagnostics</span></span>
> * <span data-ttu-id="a3df1-192">檢視主機計量</span><span class="sxs-lookup"><span data-stu-id="a3df1-192">View host metrics</span></span>
> * <span data-ttu-id="a3df1-193">啟用 hello VM 的診斷延伸模組</span><span class="sxs-lookup"><span data-stu-id="a3df1-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="a3df1-194">檢視 VM 計量</span><span class="sxs-lookup"><span data-stu-id="a3df1-194">View VM metrics</span></span>
> * <span data-ttu-id="a3df1-195">依據診斷計量建立警示</span><span class="sxs-lookup"><span data-stu-id="a3df1-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="a3df1-196">設定進階監視</span><span class="sxs-lookup"><span data-stu-id="a3df1-196">Set up advanced monitoring</span></span>

<span data-ttu-id="a3df1-197">前進 toohello 下一個教學課程的 toolearn 有關 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="a3df1-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3df1-198">管理 VM 安全性</span><span class="sxs-lookup"><span data-stu-id="a3df1-198">Manage VM security</span></span>](./tutorial-azure-security.md)
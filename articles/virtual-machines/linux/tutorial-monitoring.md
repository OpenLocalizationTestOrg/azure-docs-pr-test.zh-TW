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
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>如何在 Azure 中 Linux 虛擬機器 toomonitor

tooensure 您在 Azure 中的虛擬機器 (Vm) 正常運作，您可以檢閱開機診斷和效能度量。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 啟用 hello VM 上的開機診斷功能
> * 檢視開機診斷
> * 檢視主機計量
> * 啟用 hello VM 的診斷延伸模組
> * 檢視 VM 計量
> * 依據診斷計量建立警示
> * 設定進階監視


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="create-vm"></a>建立 VM

toosee 診斷和動作中的度量，您需要在 VM。 首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupMonitor*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

現在，使用 [az vm create](https://docs.microsoft.com/cli/azure/vm#create) 建立 VM。 hello 下列範例會建立名為的 VM *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>啟用開機診斷

Linux Vm 開機，因為 hello 開機診斷延伸模組會擷取開機輸出，並將它儲存在 Azure 儲存體。 此資料可以使用的 tootroubleshoot VM 開機問題。 當您建立使用 Azure CLI hello 的 Linux VM 時，不會自動啟用開機診斷。

之前啟用開機診斷功能，必須 toobe 儲存開機記錄檔中建立儲存體帳戶。 儲存體帳戶必須具有全域唯一的名稱，介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。 建立儲存體帳戶以 hello [az 儲存體帳戶建立](/cli/azure/storage/account#create)命令。 在此範例中，隨機字串是使用的 toocreate 獨特的儲存體帳戶名稱。 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

當啟用開機診斷功能，則需要 hello URI toohello blob 儲存體容器。 hello 下列命令查詢 hello 儲存體帳戶 tooreturn 此 URI。 hello URI 值會儲存在變數名稱*bloburi*，hello 下一個步驟中所用。

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

現在，使用 [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable) 啟用開機診斷。 hello`--storage`值為 hello blob URI 收集 hello 上一個步驟。

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>檢視開機診斷

當啟用開機診斷時，每次您停止並啟動 VM，hello hello 開機程序的相關資訊會寫入 tooa 記錄檔。 此範例中，針對第一次解除配置 hello VM 以 hello [az vm 解除配置](/cli/azure/vm#deallocate)命令，如下所示：

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

現在開始 hello VM 以 hello [az vm 啟動]( /cli/azure/vm#stop)命令，如下所示：

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

您可以取得 hello 開機診斷資料的*myVM*以 hello [az vm 開機診斷 get 開機-記錄](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log)命令，如下所示：

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>檢視主機計量

在 Azure 中有 Linux VM 專用的主機與它互動。 度量資訊會自動收集 hello 主機，而且可以檢視 hello Azure 入口網站中，如下所示：

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroupMonitor**，然後選取**myVM** hello 資源清單中。
1. toosee 如何 hello 主機 VM 正在執行中，按一下**度量**hello VM 刀鋒視窗，然後選取任何 hello *[主機]*下的度量**可用的度量**。

    ![檢視主機計量](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>安裝診斷擴充功能

> [!IMPORTANT]
> 本文件說明 2.3 版 hello Linux 診斷延伸，其中已被取代。 至 2018 年 6 月 30 日止就不再支援 2.3 版。
>
> 3.0 版的 hello Linux 診斷延伸模組可以改為啟用。 如需詳細資訊，請參閱[hello 文件](./diagnostic-extension.md)。

hello 基本主機計量可供使用，但更細微的 toosee 和特定 VM 的度量，您 tooneed tooinstall hello Azure 診斷擴充功能在 hello VM 上。 hello Azure 診斷擴充功能可讓其他監視和診斷資料 toobe hello VM 從擷取。 您可以檢視這些效能度量，並依據 hello VM 執行的方式建立警示。 hello 診斷延伸模組會安裝透過 hello Azure 入口網站，如下所示：

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
1. 按一下 [診斷設定]。 hello 清單顯示*開機診斷*已經啟用 hello 前一節。 按一下核取方塊 hello*基本度量*。
1. 在 hello*儲存體帳戶*區段中，瀏覽 tooand 選取 hello *mydiagdata [1234]* hello 前一節中所建立的帳戶。
1. 按一下 hello**儲存** 按鈕。

    ![檢視診斷計量](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>檢視 VM 計量

您可以在 hello 檢視 hello VM 度量您檢視 hello 主機 VM 計量的相同方式：

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
1. toosee 如何 hello VM 正在執行中，按一下**度量**hello VM 刀鋒視窗中，且然後選取其中一個下 hello 診斷度量**可用的度量**。

    ![檢視 VM 計量](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>建立警示

您可以根據特定效能計量來建立警示。 警示可能會使用的 toonotify 時的平均 CPU 使用率超過某個臨界值或可用的磁碟空間低於特定大小，例如。 警示會顯示在 hello Azure 入口網站，或可以透過電子郵件傳送。 您也可以在所產生的回應 tooalerts 觸發 Azure 自動化 runbook 或 Azure 邏輯應用程式。

hello 下列範例會建立警示的平均 CPU 使用量。

1. 在 hello Azure 入口網站，按一下 **資源群組**，選取**myResourceGroup**，然後選取**myVM** hello 資源清單中。
2. 按一下**警示規則**hello VM 刀鋒視窗，然後按一下**新增度量的警示**hello 的 hello 警示 刀鋒視窗的頂端。
4. 提供警示的 [名稱]，例如 myAlertRule。
5. tootrigger 警示時的 CPU 百分比超過五分鐘，1.0 會保留所有 hello 選取其他預設值。
6. （選擇性） 核取方塊 hello*電子郵件擁有者、 參與者與讀者*toosend 電子郵件通知。 hello 預設動作是 toopresent hello 入口網站中的通知。
7. 按一下 hello**確定** 按鈕。


## <a name="advanced-monitoring"></a>進階監視 

您可以使用 [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) (OMS) 對您的 VM 進行更進階的監視。 如果您尚未這麼做，可以註冊 Operations Management Suite 的[免費試用版](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial)。

當您擁有存取 toohello OMS 入口網站時，您可以在 hello 設定 刀鋒視窗上找到 hello 工作區的索引鍵和工作區識別碼。 取代 < 工作區金鑰 > 和 < 工作區識別碼 > hello 值從您的 OMS 工作區，然後您可以使用**az vm 延伸模組集**tooadd hello OMS 擴充 toohello VM:

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

在 hello 記錄搜尋刀鋒視窗中的 hello OMS 入口網站，您應該看到*myVM*例如 hello 下列圖片所示：

![OMS 刀鋒視窗](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您利用 Azure 資訊安全中心設定並檢閱 VM。 您已了解如何︰

> [!div class="checklist"]
> * 啟用 hello VM 上的開機診斷功能
> * 檢視開機診斷
> * 檢視主機計量
> * 啟用 hello VM 的診斷延伸模組
> * 檢視 VM 計量
> * 依據診斷計量建立警示
> * 設定進階監視

前進 toohello 下一個教學課程的 toolearn 有關 Azure 資訊安全中心。

> [!div class="nextstepaction"]
> [管理 VM 安全性](./tutorial-azure-security.md)
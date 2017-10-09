---
title: "aaaAzure 雲端殼層 （預覽） 快速入門 |Microsoft 文件"
description: "Hello Azure 雲端殼層的快速入門"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>使用 Azure 雲端殼層 hello 的快速入門

本文件詳述 toouse 如何在 hello hello Azure 雲端殼層[Azure 入口網站](https://ms.portal.azure.com/)。

## <a name="start-cloud-shell"></a>啟動 Cloud Shell
1. 啟動**雲端殼層**從 hello 上層導覽 hello Azure 入口網站的 <br>
![](media/shell-icon.png)
2. 選取的訂用帳戶 toocreate 儲存體帳戶和 Azure 的檔案共用
3. 選取 [建立儲存體]

> [!TIP]
> 在每個工作階段會自動驗證您以使用 Azure CLI 2.0。

### <a name="set-your-subscription"></a>設定您的訂用帳戶
1. 列出您可存取的訂用帳戶： <br>
`az account list`
2. 設定您慣用的訂用帳戶： <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> 系統將使用 `/home/<user>/.azure/azureProfile.json` 來記住您的訂用帳戶，以供未來工作階段使用。

### <a name="create-a-resource-group"></a>建立資源群組
在 WestUS 中建立名為 "MyRG" 的新資源群組： <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>建立 Linux VM
在您的新資源群組中建立 Ubuntu VM。 hello Azure CLI 2.0 將使用它們來建立 SSH 金鑰和安裝 hello VM。 <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> hello VM 會置於所使用的公用和私用金鑰 tooauthenticate`/User/.ssh/id_rsa`和`/User/.ssh/id_rsa.pub`預設 Azure CLI 2.0。 您的 .ssh 資料夾會保存在所連接 Azure 檔案共用的 5-GB 映像中。

您在此 VM 上的使用者名稱，將會是用於 Cloud Shell 中的使用者名稱 ($User@Azure:)。

### <a name="ssh-into-your-linux-vm"></a>透過 SSH 連線到您的 Linux VM
1. 搜尋您在 hello Azure 入口網站搜尋列中的 VM 名稱
2. 按一下 [連線] 然後執行：`ssh username@ipaddress`

![](media/sshcmd-copy.png)

在建立 hello SSH 連線，您應該會看到 hello Ubuntu 歡迎畫面提示。
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>清除 
刪除您的資源群組以及其中的任何資源： <br>
執行 `az group delete -n MyRG`

## <a name="next-steps"></a>後續步驟
[了解如何在 Cloud Shell 上保存儲存體](persisting-shell-storage.md) <br>
[了解 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) \(英文\) <br>
[了解 Azure 檔案儲存體](../storage/files/storage-files-introduction.md) <br>
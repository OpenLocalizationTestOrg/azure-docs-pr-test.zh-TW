---
title: "在 Azure 中的 Windows VM 上 MongoDB aaaInstall |Microsoft 文件"
description: "了解如何 tooinstall MongoDB Azure VM 上建立執行 Windows Server 的 hello 傳統部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>在 Azure 中的 Windows VM 上安裝 MongoDB
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。  本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 tooinstall 和設定 MongoDB 使用 hello Resource Manager 部署模型，請參閱[本文](../install-mongodb.md)。

[MongoDB][MongoDB] 是一個受歡迎的高效能開放原始碼 NoSQL 資料庫。 這篇文章會引導您完成建立 Windows Server 虛擬機器 (VM) 使用 hello [Azure 入口網站][AzurePortal]。 然後，您會建立並附加資料磁碟 toohello VM 安裝和設定 MongoDB 之前。 如果您希望 toouse Azure 中有現有的 VM，您可以跳過直接[安裝和設定 MongoDB](#install-and-run-mongodb-on-the-virtual-machine)。

## <a name="create-a-virtual-machine-running-windows-server"></a>建立執行 Windows Server 的虛擬機器
請遵循這些指示 toocreate 虛擬機器。

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> 您可以新增 MongoDB 端點時建立 hello 的虛擬機器，並設定它，如下所示： 名稱為**Mongo**，使用**TCP**為 hello 通訊協定，並設定 hello 公用和私用連接埠太**27017**。
>
>

## <a name="attach-a-data-disk"></a>連接資料磁碟
tooprovide 儲存體 hello 虛擬機器，將資料磁碟連接，並再將它初始化，因此 Windows 才能使用它。 如果您已經有資料磁碟，您可以連接現有的磁碟，或可以連接空的磁碟。

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

初始化 hello 磁碟上的指示，請參閱 「 如何： 初始化新的資料磁碟在 Windows 伺服器 」 中[tooattach 資料磁碟 tooa Windows 虛擬機器的如何](attach-disk.md)。

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>安裝並執行 MongoDB hello 虛擬機器上
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>摘要
在此教學課程中，您將學會如何 toocreate 執行 Windows Server 的虛擬機器從遠端連接 tooit，並連接資料磁碟。  您也學到如何 tooinstall 和 hello Windows 型虛擬機器上設定 MongoDB。 您現在可以存取 MongoDB hello Windows 型虛擬機器上，藉由下列進階主題 hello 中的 hello [MongoDB 文件][MongoDocs]。

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/


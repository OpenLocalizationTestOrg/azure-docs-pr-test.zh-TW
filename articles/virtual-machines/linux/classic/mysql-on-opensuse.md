---
title: "aaaInstall OpenSUSE VM 上的 MySQL |Microsoft 文件"
description: "了解在 Azure 中 OpenSUSE Linux VMirtual 機器上的 MySQL tooinstall。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a>在 Azure 中執行 OpenSUSE Linux 的虛擬機器上安裝 MySQL
[MySQL][MySQL] 是一種很受歡迎的開放原始碼 SQL 資料庫。 此教學課程會示範如何 toocreate 執行 OpenSUSE Linux 的虛擬機器再安裝 MySQL。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a>建立執行 OpenSUSE Linux 的虛擬機器
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a>安裝並執行 hello 虛擬機器上的 MySQL
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a>後續步驟
如需 MySQL 的詳細資訊，請參閱 hello [MySQL 文件][MySQLDocs]。

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com


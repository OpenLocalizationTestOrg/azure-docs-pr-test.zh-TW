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
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="192a8-103">在 Azure 中執行 OpenSUSE Linux 的虛擬機器上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="192a8-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="192a8-104">[MySQL][MySQL] 是一種很受歡迎的開放原始碼 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="192a8-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="192a8-105">此教學課程會示範如何 toocreate 執行 OpenSUSE Linux 的虛擬機器再安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="192a8-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="192a8-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="192a8-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="192a8-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="192a8-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="192a8-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="192a8-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="192a8-109">建立執行 OpenSUSE Linux 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="192a8-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="192a8-110">安裝並執行 hello 虛擬機器上的 MySQL</span><span class="sxs-lookup"><span data-stu-id="192a8-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="192a8-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="192a8-111">Next steps</span></span>
<span data-ttu-id="192a8-112">如需 MySQL 的詳細資訊，請參閱 hello [MySQL 文件][MySQLDocs]。</span><span class="sxs-lookup"><span data-stu-id="192a8-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com


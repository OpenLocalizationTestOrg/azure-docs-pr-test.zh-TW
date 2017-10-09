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
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="d5868-103">在 Azure 中的 Windows VM 上安裝 MongoDB</span><span class="sxs-lookup"><span data-stu-id="d5868-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d5868-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d5868-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d5868-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d5868-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d5868-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="d5868-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d5868-107">tooinstall 和設定 MongoDB 使用 hello Resource Manager 部署模型，請參閱[本文](../install-mongodb.md)。</span><span class="sxs-lookup"><span data-stu-id="d5868-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="d5868-108">[MongoDB][MongoDB] 是一個受歡迎的高效能開放原始碼 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d5868-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="d5868-109">這篇文章會引導您完成建立 Windows Server 虛擬機器 (VM) 使用 hello [Azure 入口網站][AzurePortal]。</span><span class="sxs-lookup"><span data-stu-id="d5868-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="d5868-110">然後，您會建立並附加資料磁碟 toohello VM 安裝和設定 MongoDB 之前。</span><span class="sxs-lookup"><span data-stu-id="d5868-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="d5868-111">如果您希望 toouse Azure 中有現有的 VM，您可以跳過直接[安裝和設定 MongoDB](#install-and-run-mongodb-on-the-virtual-machine)。</span><span class="sxs-lookup"><span data-stu-id="d5868-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="d5868-112">建立執行 Windows Server 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d5868-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="d5868-113">請遵循這些指示 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d5868-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="d5868-114">您可以新增 MongoDB 端點時建立 hello 的虛擬機器，並設定它，如下所示： 名稱為**Mongo**，使用**TCP**為 hello 通訊協定，並設定 hello 公用和私用連接埠太**27017**。</span><span class="sxs-lookup"><span data-stu-id="d5868-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="d5868-115">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="d5868-115">Attach a data disk</span></span>
<span data-ttu-id="d5868-116">tooprovide 儲存體 hello 虛擬機器，將資料磁碟連接，並再將它初始化，因此 Windows 才能使用它。</span><span class="sxs-lookup"><span data-stu-id="d5868-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="d5868-117">如果您已經有資料磁碟，您可以連接現有的磁碟，或可以連接空的磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5868-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="d5868-118">初始化 hello 磁碟上的指示，請參閱 「 如何： 初始化新的資料磁碟在 Windows 伺服器 」 中[tooattach 資料磁碟 tooa Windows 虛擬機器的如何](attach-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="d5868-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="d5868-119">安裝並執行 MongoDB hello 虛擬機器上</span><span class="sxs-lookup"><span data-stu-id="d5868-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="d5868-120">摘要</span><span class="sxs-lookup"><span data-stu-id="d5868-120">Summary</span></span>
<span data-ttu-id="d5868-121">在此教學課程中，您將學會如何 toocreate 執行 Windows Server 的虛擬機器從遠端連接 tooit，並連接資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5868-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="d5868-122">您也學到如何 tooinstall 和 hello Windows 型虛擬機器上設定 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="d5868-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="d5868-123">您現在可以存取 MongoDB hello Windows 型虛擬機器上，藉由下列進階主題 hello 中的 hello [MongoDB 文件][MongoDocs]。</span><span class="sxs-lookup"><span data-stu-id="d5868-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/


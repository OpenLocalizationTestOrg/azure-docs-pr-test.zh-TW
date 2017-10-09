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
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="0bc17-103">使用 Azure 雲端殼層 hello 的快速入門</span><span class="sxs-lookup"><span data-stu-id="0bc17-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="0bc17-104">本文件詳述 toouse 如何在 hello hello Azure 雲端殼層[Azure 入口網站](https://ms.portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0bc17-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="0bc17-105">啟動 Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="0bc17-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="0bc17-106">啟動**雲端殼層**從 hello 上層導覽 hello Azure 入口網站的</span><span class="sxs-lookup"><span data-stu-id="0bc17-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="0bc17-107">選取的訂用帳戶 toocreate 儲存體帳戶和 Azure 的檔案共用</span><span class="sxs-lookup"><span data-stu-id="0bc17-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="0bc17-108">選取 [建立儲存體]</span><span class="sxs-lookup"><span data-stu-id="0bc17-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="0bc17-109">在每個工作階段會自動驗證您以使用 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="0bc17-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="0bc17-110">設定您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0bc17-110">Set your subscription</span></span>
1. <span data-ttu-id="0bc17-111">列出您可存取的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="0bc17-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="0bc17-112">設定您慣用的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="0bc17-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="0bc17-113">系統將使用 `/home/<user>/.azure/azureProfile.json` 來記住您的訂用帳戶，以供未來工作階段使用。</span><span class="sxs-lookup"><span data-stu-id="0bc17-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="0bc17-114">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0bc17-114">Create a resource group</span></span>
<span data-ttu-id="0bc17-115">在 WestUS 中建立名為 "MyRG" 的新資源群組：</span><span class="sxs-lookup"><span data-stu-id="0bc17-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="0bc17-116">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0bc17-116">Create a Linux VM</span></span>
<span data-ttu-id="0bc17-117">在您的新資源群組中建立 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="0bc17-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="0bc17-118">hello Azure CLI 2.0 將使用它們來建立 SSH 金鑰和安裝 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0bc17-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="0bc17-119">hello VM 會置於所使用的公用和私用金鑰 tooauthenticate`/User/.ssh/id_rsa`和`/User/.ssh/id_rsa.pub`預設 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="0bc17-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="0bc17-120">您的 .ssh 資料夾會保存在所連接 Azure 檔案共用的 5-GB 映像中。</span><span class="sxs-lookup"><span data-stu-id="0bc17-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="0bc17-121">您在此 VM 上的使用者名稱，將會是用於 Cloud Shell 中的使用者名稱 ($User@Azure:)。</span><span class="sxs-lookup"><span data-stu-id="0bc17-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="0bc17-122">透過 SSH 連線到您的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="0bc17-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="0bc17-123">搜尋您在 hello Azure 入口網站搜尋列中的 VM 名稱</span><span class="sxs-lookup"><span data-stu-id="0bc17-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="0bc17-124">按一下 [連線] 然後執行：`ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="0bc17-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="0bc17-125">在建立 hello SSH 連線，您應該會看到 hello Ubuntu 歡迎畫面提示。</span><span class="sxs-lookup"><span data-stu-id="0bc17-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="0bc17-126">清除</span><span class="sxs-lookup"><span data-stu-id="0bc17-126">Cleaning up</span></span> 
<span data-ttu-id="0bc17-127">刪除您的資源群組以及其中的任何資源：</span><span class="sxs-lookup"><span data-stu-id="0bc17-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="0bc17-128">執行 `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="0bc17-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bc17-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bc17-129">Next Steps</span></span>
[<span data-ttu-id="0bc17-130">了解如何在 Cloud Shell 上保存儲存體</span><span class="sxs-lookup"><span data-stu-id="0bc17-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="0bc17-131">
[了解 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="0bc17-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="0bc17-132">
[了解 Azure 檔案儲存體](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="0bc17-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>
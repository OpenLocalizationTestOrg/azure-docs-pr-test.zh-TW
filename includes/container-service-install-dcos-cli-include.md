---
title: "aaaInstall hello DC/OS CLI |Microsoft 文件"
description: "安裝 hello DC/OS CLI。"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "容器, 微服務, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="af6bb-104">這適用於使用 DC/OS 型 ACS 叢集時。</span><span class="sxs-lookup"><span data-stu-id="af6bb-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="af6bb-105">沒有任何需要 toodo 這適用於群集為基礎的 ACS 叢集。</span><span class="sxs-lookup"><span data-stu-id="af6bb-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="af6bb-106">首先， [tooyour DC/作業系統為基礎的 ACS 叢集連線](../articles/container-service/container-service-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="af6bb-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="af6bb-107">一旦您已這麼做，您可以在下列 hello 命令與用戶端電腦上安裝 hello DC/OS CLI:</span><span class="sxs-lookup"><span data-stu-id="af6bb-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="af6bb-108">如果您使用舊版 Python，您可能會注意到一些 "InsecurePlatformWarnings"。</span><span class="sxs-lookup"><span data-stu-id="af6bb-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="af6bb-109">您可以放心地忽略這些警告。</span><span class="sxs-lookup"><span data-stu-id="af6bb-109">You can safely ignore these.</span></span>

<span data-ttu-id="af6bb-110">在不需要重新啟動您的殼層啟動順序 tooget，執行：</span><span class="sxs-lookup"><span data-stu-id="af6bb-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="af6bb-111">當您啟動新殼層時，就不需要此步驟。</span><span class="sxs-lookup"><span data-stu-id="af6bb-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="af6bb-112">現在您可以確認已安裝 CLI 該 hello:</span><span class="sxs-lookup"><span data-stu-id="af6bb-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```
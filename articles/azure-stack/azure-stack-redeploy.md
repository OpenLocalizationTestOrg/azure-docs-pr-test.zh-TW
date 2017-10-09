---
title: "aaaRedeploy Azure 堆疊 |Microsoft 文件"
description: "重新部署 Azure Stack。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: ec26745bcb54edd7c26960eec55d41504aff1911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-azure-stack"></a><span data-ttu-id="6cfae-103">重新部署 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6cfae-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="6cfae-104">tooredeploy Azure 堆疊，您必須透過從頭開始，如下所述。</span><span class="sxs-lookup"><span data-stu-id="6cfae-104">tooredeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-tooredeploy-azure-stack"></a><span data-ttu-id="6cfae-105">步驟 tooredeploy Azure 堆疊</span><span class="sxs-lookup"><span data-stu-id="6cfae-105">Steps tooredeploy Azure Stack</span></span>
1. <span data-ttu-id="6cfae-106">Hello 開發套件在主機上，開啟提升權限的 PowerShell 主控台 > 瀏覽 toohello asdk installer.ps1 指令碼 > 執行此程式碼 > 按一下**重新開機**。</span><span class="sxs-lookup"><span data-stu-id="6cfae-106">On hello development kit host, open an elevated PowerShell console > navigate toohello asdk-installer.ps1 script > run it > click **Reboot**.</span></span>
2. <span data-ttu-id="6cfae-107">選取 hello 基礎作業系統 (不**Azure 堆疊**) 按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6cfae-107">Select hello base operating system (not **Azure Stack**) and click **Next**.</span></span>
3. <span data-ttu-id="6cfae-108">Hello 開發套件主機重新開機之後，刪除 hello CloudBuilder.vhdx 檔案已用來作為 hello 先前部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="6cfae-108">After hello development kit host reboots, delete hello CloudBuilder.vhdx file that was used as part of hello previous deployment.</span></span>
4. <span data-ttu-id="6cfae-109">[部署 hello 開發套件](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="6cfae-109">[Deploy hello development kit](azure-stack-run-powershell-script.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cfae-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6cfae-110">Next steps</span></span>
[<span data-ttu-id="6cfae-111">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="6cfae-111">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)


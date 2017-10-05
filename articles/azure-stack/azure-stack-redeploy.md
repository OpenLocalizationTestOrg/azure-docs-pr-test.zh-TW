---
title: "重新部署 Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: 891cde9b16bbbb51729129b6ad7a0f3794307baa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="redeploy-azure-stack"></a><span data-ttu-id="5c14d-103">重新部署 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5c14d-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="5c14d-104">若要重新部署 Azure Stack，您必須從頭開始進行，如下所述。</span><span class="sxs-lookup"><span data-stu-id="5c14d-104">To redeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-to-redeploy-azure-stack"></a><span data-ttu-id="5c14d-105">重新部署 Azure Stack 的步驟</span><span class="sxs-lookup"><span data-stu-id="5c14d-105">Steps to redeploy Azure Stack</span></span>
1. <span data-ttu-id="5c14d-106">在開發套件主機上，開啟提升權限的 PowerShell 主控台 > 瀏覽至 asdk installer.ps1 指令碼 > 執行此程式碼 > 按一下 [重新開機]。</span><span class="sxs-lookup"><span data-stu-id="5c14d-106">On the development kit host, open an elevated PowerShell console > navigate to the asdk-installer.ps1 script > run it > click **Reboot**.</span></span>
2. <span data-ttu-id="5c14d-107">選取基礎作業系統 (非 Azure Stack) 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5c14d-107">Select the base operating system (not **Azure Stack**) and click **Next**.</span></span>
3. <span data-ttu-id="5c14d-108">開發套件主機重新開機之後，刪除先前部署過程中所使用的 CloudBuilder.vhdx 檔案。</span><span class="sxs-lookup"><span data-stu-id="5c14d-108">After the development kit host reboots, delete the CloudBuilder.vhdx file that was used as part of the previous deployment.</span></span>
4. <span data-ttu-id="5c14d-109">[部署開發套件](azure-stack-run-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="5c14d-109">[Deploy the development kit](azure-stack-run-powershell-script.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c14d-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c14d-110">Next steps</span></span>
[<span data-ttu-id="5c14d-111">連接至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5c14d-111">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)


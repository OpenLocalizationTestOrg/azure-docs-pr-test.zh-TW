---
title: "在 Linux 虛擬機器上的 aaaUse 根權限 |Microsoft 文件"
description: "了解 toouse 根在 Azure 中 Linux 虛擬機器上的權限。"
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>在 Azure 中的 Linux 虛擬機器上使用根權限
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

根據預設，hello`root`在 Azure 中 Linux 虛擬機器上停用使用者。 使用者可以執行使用更高權限命令使用 hello`sudo`命令。 不過，hello 經驗會根據 hello 系統已佈建方式而有所不同。

1. **SSH 金鑰和密碼只能使用 OR 密碼**-hello 虛擬機器佈建並提供兩個憑證 (`.CER`檔案) 或 SSH 金鑰，以及密碼，或只要使用者名稱與密碼。 在此情況下`sudo`會提示輸入 hello 使用者的密碼，然後再執行 hello 命令。
2. **僅使用 SSH 金鑰**-hello 虛擬機器所使用的憑證佈建 (`.cer`， `.pem`，或`.pub`檔案) 或 SSH 金鑰，但沒有密碼。  在此情況下`sudo`**則不會**hello 使用者的密碼，才能執行 hello 命令提示。

## <a name="ssh-key-and-password-or-password-only"></a>SSH 金鑰和密碼，或僅密碼
登入使用 SSH 金鑰或密碼驗證時，hello Linux 虛擬機器，然後再執行命令使用`sudo`，例如：

    # sudo <command>
    [sudo] password for azureuser:

在此情況下 hello 使用者將會提示輸入密碼。 輸入 hello 密碼之後`sudo`會執行與 hello 命令`root`權限。

您也可以藉由編輯 hello 啟用 passwordless sudo`/etc/sudoers.d/waagent`檔案，例如：

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

這項變更可讓 passwordless sudo hello 使用者 」 azureuser"。

## <a name="ssh-key-only"></a>僅 SSH 金鑰
登入 hello Linux 虛擬機器使用 SSH 金鑰驗證，然後再執行命令使用`sudo`，例如：

    # sudo <command>

在此情況下 hello 使用者將**不**提示輸入密碼。 按下之後`<enter>`，`sudo`會執行與 hello 命令`root`權限。


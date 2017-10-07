---
title: "PowerShell toocreate hello Marketplace 的 VM 上 aaaSet |Microsoft 文件"
description: "設定 Azure PowerShell，以及使用選擇性程序的指示，toocreate VM 映像 toodeploy 和上銷售，hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>設定 Azure PowerShell toocreate hello Azure Marketplace 供應項目
如需詳細資訊 tooset 向上 PowerShell 在 Azure 中，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 一個簡單的方法是 toouse hello 憑證方法，它會下載並匯入進行驗證所需的憑證。 tooobtain hello 所需的憑證，請使用 hello **Get-azurepublishsettingsfile** cmdlet。 當系統提示您輸入時，請儲存 hello 檔案。 tooimport hello 憑證到 PowerShell 工作階段，使用 hello **Import-azurepublishsettingsfile** cmdlet。

tooconfigure 和市集 hello Microsoft Azure 訂用帳戶的一般設定 hello PowerShell 工作階段，使用 hello**組 AzureSubscription**和**Select-azuresubscription** cmdlet:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

hello 第一個命令會將預設儲存體帳戶關聯 hello 訂用帳戶 （在某些 VM 佈建作業時需要）。  hello 第二個可讓 hello hello （辨識其他的 cmdlet） 的其中一個目前的訂用帳戶。

## <a name="see-also"></a>另請參閱
* [快速入門： 如何 toopublish 優惠 toohello Azure Marketplace](marketplace-publishing-getting-started.md)
* [建立虛擬機器映像的 hello Marketplace](marketplace-publishing-vm-image-creation.md)


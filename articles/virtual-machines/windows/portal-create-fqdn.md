---
title: "針對 Windows VM 中 hello Azure 入口網站的 FQDN aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 完整網域名稱或 FQDN，資源管理員的基礎 hello Azure 入口網站中的虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>針對 Windows VM 建立 hello Azure 入口網站中的完整的網域名稱

當您建立虛擬機器 (VM) 在 hello [Azure 入口網站](https://portal.azure.com)，會自動建立 hello 虛擬機器的公用 IP 資源。 您使用此 IP 位址 tooremotely 存取 hello VM。 雖然 hello 入口網站並不會建立[完整的網域名稱](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)，或 FQDN，您可以建立一個 hello VM 建立之後。 本文示範 hello 步驟 toocreate DNS 名稱或 FQDN。

## <a name="create-a-fqdn"></a>建立 FQDN
此文章假設您已經建立一個 VM。 如有需要您可以[hello 入口網站中建立的 VM](quick-create-portal.md)或[使用 Azure PowerShell](quick-create-powershell.md)。 在您的 VM 已啟動並執行之後，請遵循下列步驟：

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

您現在可以連線從遠端 toohello VM 使用這類的此 DNS 名稱的遠端桌面通訊協定 (RDP)。

## <a name="next-steps"></a>後續步驟
既然您的 VM 已經有公用 IP 和 DNS 名稱，您便可以部署通用應用程式架構或服務，例如 IIS、SQL 或 SharePoint。

您也可以進一步閱讀[使用 Resource Manager](../../azure-resource-manager/resource-group-overview.md)，以取得建置 Azure 部署的相關秘訣。


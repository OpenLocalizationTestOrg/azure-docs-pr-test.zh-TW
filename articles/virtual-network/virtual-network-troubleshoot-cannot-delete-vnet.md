---
title: "aaaCannot 刪除 Azure 中的虛擬網路 |Microsoft 文件"
description: "了解如何 tootroubleshoot hello 無法刪除 Azure 中的虛擬網路的問題。"
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>疑難排解： 無法 toodelete Azure 中的虛擬網路

當您嘗試 toodelete Microsoft Azure 中的虛擬網路時，您可能會收到錯誤。 本文章提供疑難排解步驟 toohelp 解決這個問題。 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>疑難排解指引 

1. [檢查是否正在執行 hello 虛擬網路中的虛擬網路閘道](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network)。
2. [檢查是否正在執行 hello 虛擬網路中的應用程式閘道](#check-whether-an-application-gateway-is-running-in-the-virtual-network)。
3. [檢查是否已啟用 hello 虛擬網路中的 Azure Active Directory 網域服務](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network)。
4. [檢查 hello 虛擬網路是否連線的 tooother 資源](#check-whether-the-virtual-network-is-connected-to-other-resource)。
5. [請檢查虛擬機器是否仍在執行 hello 虛擬網路中](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network)。
6. [檢查 hello 虛擬網路是否陷入移轉](#check-whether-the-virtual-network-is-stuck-in-migration)。

## <a name="troubleshooting-steps"></a>疑難排解步驟

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>檢查是否正在執行 hello 虛擬網路中的虛擬網路閘道

tooremove hello 虛擬網路，您必須先移除 hello 虛擬網路閘道。

傳統的虛擬網路，請移 toohello**概觀**hello 傳統中虛擬網路的 hello Azure 入口網站頁面。 在 hello **VPN 連線**區段中，如果 hello 閘道正在執行 hello 虛擬網路中，您會看到 hello IP hello 閘道位址。 

![檢查閘道是否正在執行](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

虛擬網路，請移 toohello**概觀**hello 虛擬網路的頁面。 請檢查**連接的裝置**hello 虛擬網路閘道。

![檢查 hello 連接的裝置](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

您可以移除 hello 閘道之前，先移除任何**連接**hello 閘道中的物件。 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>檢查是否正在執行 hello 虛擬網路中的應用程式閘道

移 toohello**概觀**hello 虛擬網路的頁面。 檢查 hello**連接的裝置**hello 應用程式閘道。

![檢查 hello 連接的裝置](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

如果沒有應用程式閘道，您必須移除它，才能刪除 hello 虛擬網路。

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>檢查是否已啟用 hello 虛擬網路中的 Azure Active Directory 網域服務

如果已啟用，且已連線的 toohello 虛擬網路 hello Active Directory 網域服務，您無法刪除此虛擬網路。 

![檢查 hello 連接的裝置](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable hello 服務，請遵循下列步驟：

1. 移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左窗格中，選取**Active Directory**。
3. 選取已啟用的 Active Directory 網域服務的 hello Azure Active Directory (Azure AD) 目錄。
4. 選取 hello**設定** 索引標籤。
5. 在下**網域服務**，變更 hello**啟用這個目錄的網域服務**太選項**否**。  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>檢查 hello 虛擬網路是否連線的 tooother 資源

檢查線路連結、連線和虛擬網路對等互連。 任何一項都可能會造成虛擬網路刪除 toofail。 

hello 建議的刪除順序如下所示：

1. 閘道連線
2. 閘道
3. IP
4. 虛擬網路對等互連
5. App Service Environment (ASE)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>請檢查虛擬機器是否仍在執行中 hello 虛擬網路

請確定沒有虛擬機器 hello 虛擬網路。

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>檢查 hello 虛擬網路是否陷入移轉

如果 hello 虛擬網路卡在移轉狀態，無法刪除。 執行 hello 命令 tooabort hello 在移轉之後，然後再刪除 hello 虛擬網路。

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>後續步驟

- [Azure 虛擬網路](virtual-networks-overview.md)
- [Azure 虛擬網路的常見問題 (FAQ)](virtual-networks-faq.md)
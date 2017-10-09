---
title: "在 Azure 中的 aaaCreate SharePoint 伺服器陣列 |Microsoft 文件"
description: "快速建立新的 SharePoint 2013 或 SharePoint 2016 伺服器陣列在 Azure 中使用 hello Azure marketplace 入口網站所提供。"
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>建立使用 hello Azure marketplace 入口網站所提供的 SharePoint 伺服器陣列

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>SharePoint 2013 伺服器陣列
您可以使用 Microsoft Azure 入口網站 marketplace hello，快速建立預先設定的 SharePoint Server 2013 伺服器陣列。 當您在開發/測試環境中需要基本或高可用性 SharePoint 伺服器陣列時，或是您要評估將 SharePoint Server 2013 做為組織的共同作業方案時，這將可為您省下許多時間。

> [!NOTE]
> hello **SharePoint 伺服器陣列**hello Azure Marketplace 中的 hello Azure 入口網站的項目已經移除。 它已被取代 hello **SharePoint 2013 非高可用性伺服器陣列**和**SharePoint 2013 的高可用性伺服器陣列**項目。
>
>

hello 基本的 SharePoint 伺服器陣列包含在此組態中的三部虛擬機器。

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

此伺服器陣列組態可用於 SharePoint 應用程式開發的簡化設定，或用於您第一次的 SharePoint 2013 評估。

toocreate hello 基本 （三部伺服器） SharePoint 伺服陣列：

1. 按一下 [ [這裡](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)]。
2. 按一下 [ **部署**]。
3. 在 hello **SharePoint 2013 非高可用性伺服器陣列** 窗格中，按一下 **建立**。
4. 指定設定的 hello hello 步驟**建立 SharePoint 2013 非高可用性伺服器陣列** 窗格中，然後再按一下**建立**。

hello 高可用性 SharePoint 伺服器陣列包含在此組態的九個虛擬機器。

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

您可以使用此伺服器陣列組態 tootest 更高版本用戶端負載、 hello 外部 SharePoint 網站的高可用性和 SQL Server AlwaysOn 可用性群組的 SharePoint 伺服器陣列。 此組態也可用於高可用性環境中的 SharePoint 應用程式開發。

toocreate hello 高可用性 （九伺服器） SharePoint 伺服陣列：

1. 按一下 [ [這裡](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)]。
2. 按一下 [ **部署**]。
3. 在 hello **SharePoint 2013 的高可用性伺服器陣列** 窗格中，按一下 **建立**。
4. 在 [hello hello 七個步驟中指定設定**建立 SharePoint 2013 HA 陣列**] 窗格中，然後再按一下**建立**。

> [!NOTE]
> 您無法建立 hello **SharePoint 2013 非高可用性伺服器陣列**或**SharePoint 2013 的高可用性伺服器陣列**Azure 免費試用版。
>
>

hello Azure 入口網站會建立這兩個這些伺服器陣列中純雲端虛擬網路與網際網路對向網頁存在。 沒有站對站 VPN 或 ExpressRoute 連線後 tooyour 組織網路。

> [!NOTE]
> 當您建立 hello 基本或高可用性 SharePoint 伺服器陣列使用 hello Azure 入口網站，您不能指定現有的資源群組。 toowork 這項限制，使用 Azure PowerShell 建立這些陣列。 如需詳細資訊，請參閱[使用 Azure PowerShell 建立 SharePoint 2013 開發/測試陣列](https://technet.microsoft.com/library/mt743093.aspx#powershell)。
>
>

## <a name="sharepoint-2016-farms"></a>SharePoint 2016 伺服器陣列
請參閱[本文](https://technet.microsoft.com/library/mt723354.aspx)hello 指示 toobuild hello 遵循單一伺服器 SharePoint Server 2016 伺服器陣列。

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>管理 hello SharePoint 伺服器陣列
您可以管理這些伺服器陣列，透過遠端桌面連線的 hello 伺服器。 如需詳細資訊，請參閱[登入 toohello 虛擬機器](quick-create-portal.md#connect-to-virtual-machine)。

從 hello 中央系統管理 SharePoint 網站上，您可以設定我的網站、 SharePoint 應用程式及其他功能。 如需詳細資訊，請參閱 [設定 SharePoint](http://technet.microsoft.com/library/ee836142.aspx)。

## <a name="next-steps"></a>後續步驟
* 探索 Azure 基礎結構服務中的其他 [SharePoint 組態](https://technet.microsoft.com/library/dn635309.aspx) 。

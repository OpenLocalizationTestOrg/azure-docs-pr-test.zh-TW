---
title: "aaaSQL Server 可用性群組-Azure 虛擬機器-概觀 |Microsoft 文件"
description: "本文介紹 Azure 虛擬機器上的「SQL Server 可用性群組」。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Azure 虛擬機器上的 SQL Server Always On 可用性群組簡介 #

本文介紹 Azure 虛擬機器上的 SQL Server 可用性群組。 

Always On 可用性群組在 Azure 虛擬機器都類似 tooAlways 在內部部署可用性群組。 如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)。 

hello 圖表說明完成 SQL Server 可用性群組的 Azure 虛擬機器中的 hello 組件。

![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

hello 主要差異為可用性群組在 Azure 虛擬機器中的 hello Azure 虛擬機器，需要[負載平衡器](../../../load-balancer/load-balancer-overview.md)。 hello 負載平衡器會保存 hello hello 可用性群組接聽程式的 IP 位址。 如果您有多個可用性群組，則每個群組都需要一個接聽程式。 一個負載平衡器可以支援多個接聽程式。

當您準備好 toobuild SQL Server 可用性 aroup Azure 虛擬機器上，請參閱 toothese 教學課程。

## <a name="automatically-create-an-availability-group-from-a-template"></a>從範本自動建立可用性群組

[在 Azure VM 中自動設定 Always On 可用性群組 - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>在 Azure 入口網站中手動建立可用性群組

您也可以建立 hello 虛擬機器自行不 hello 範本。 請先完成 hello 必要條件，再建立 hello 可用性群組。 請參閱下列主題中的 hello: 

- [設定 Azure 虛擬機器上 SQL Server Always On 可用性群組的必要條件](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [建立 Alwayson 可用性群組 tooimprove 可用性和災害復原](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>後續步驟

[在不同區域中的 Azure 虛擬機器上設定 SQL Server Always On 可用性群組](virtual-machines-windows-portal-sql-availability-group-dr.md)。

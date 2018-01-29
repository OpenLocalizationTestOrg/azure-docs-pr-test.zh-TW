---
title: "Azure 保留執行個體的 Windows 軟體成本 | Microsoft Docs"
description: "了解 Windows 軟體在有保留執行個體資格的 Windows 虛擬機器中，會使用哪些計量。"
services: billing
documentationcenter: 
author: manish-shukla01
manager: manshuk
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/03/2017
ms.author: manshuk
ms.openlocfilehash: b985e6e9575ffeedcac5bcb3f94a43d23fdbb85e
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2017
---
# <a name="windows-software-costs-not-included-with-reserved-instances"></a>Windows 軟體的成本不包括在保留執行個體內

如果您的保留執行個體虛擬機器上沒有 Azure Hybrid Use Benefit，則您須為下表所列的 Windows 軟體計量支付費用：

| 計量識別碼 | 使用量檔案中的計量名稱 | 適用的虛擬機器 |
| ------- | ------------------------| --- |
| e7e152ac-f29c-4cce-ad6e-026192c01ef2 | Reservation-Windows Svr Burst (1 核心) | B 系列 |
| cac255a2-9f0f-4c62-8bd6-f0fa449c5f76 | Reservation-Windows Svr Burst (2 核心) | B 系列 |
| 09756b58-3fb5-4390-976d-9ddd14f9ed18 | Reservation-Windows Svr Burst (4 核心) | B 系列 |
| e828cb37-5920-4dc7-b30f-664e4dbcb6c7 | Reservation-Windows Svr Burst (8 核心) | B 系列 |
| f65a06cf-c9c3-47a2-8104-f17a8542215a | Reservation-Windows Svr (1 核心) | B 系列以外皆適用 |
| b99d40ae-41fe-4d1d-842b-56d72f3d15ee | Reservation-Windows Svr (2 核心) | B 系列以外皆適用 |
| 1cb88381-0905-4843-9ba2-7914066aabe5 | Reservation-Windows Svr (4 核心) | B 系列以外皆適用 |
| 07d9e10d-3e3e-4672-ac30-87f58ec4b00a | Reservation-Windows Svr (6 核心) | B 系列以外皆適用 |
| 603f58d1-1e96-460b-a933-ce3775ac7e2e | Reservation-Windows Svr (8 核心) | B 系列以外皆適用 |
| 36aaadda-da86-484a-b465-c8b5ab292d71 | Reservation-Windows Svr (12 核心) | B 系列以外皆適用 |
| 02968a6b-1654-4495-ada6-13f378ba7172 | Reservation-Windows Svr (16 核心) | B 系列以外皆適用 |
| 175434d8-75f9-474b-9906-5d151b6bed84 | Reservation-Windows Svr (20 核心) | B 系列以外皆適用 |
| 77eb6dd0-88f5-4a16-ab39-05d1742efb25 | Reservation-Windows Svr (24 核心) | B 系列以外皆適用 |
| 0d5bdf46-b719-4b1f-a780-b9bdfffd0591 | Reservation-Windows Svr (32 核心) | B 系列以外皆適用 |
| f1214b5c-cc16-445f-be6c-a3bb75f8395a | Reservation-Windows Svr (40 核心) | B 系列以外皆適用 |
| 637b7c77-65ad-4486-9cc7-dc7b3e9a8731 | Reservation-Windows Svr (64 核心) | B 系列以外皆適用 |
| da612742-e7cc-4ca3-9334-0fb7234059cd | Reservation-Windows Svr (72 核心) | B 系列以外皆適用 |
| a485cb8c-069b-4cf3-9a8e-ddd84b323da2 | Reservation-Windows Svr (128 核心) | B 系列以外皆適用 |
| 904c5c71-1eb7-43a6-961c-d305a9681624 | Reservation-Windows Svr (256 核心) | B 系列以外皆適用 |
| 6fdab81b-4284-4df9-8939-c237cc7462fe | Reservation-Windows Svr (96 核心) | B 系列以外皆適用 |

您可以透過 Azure RateCard API 來取得這些計量中每一個的成本。 如需如何取得 Azure 計量表費率的資訊，請參閱[取得 Azure 訂用帳戶中所使用資源的價格和中繼資料資訊](https://msdn.microsoft.com/library/azure/mt219004)。
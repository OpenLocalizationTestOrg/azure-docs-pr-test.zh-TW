---
title: "Windows 驗證和 Azure MFA Server | Microsoft Docs"
description: "此 Azure Multi-Factor Authentication 頁面協助您部署 Windows 驗證與 Azure Multi-Factor Authentication Server。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="1a787-103">Windows 驗證與 Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="1a787-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="1a787-104">使用 Azure Multi-Factor Authentication Server 的 [Windows 驗證] 區段來啟用及設定應用程式的 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1a787-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="1a787-105">在設定 Windows 驗證之前，請注意下列清單︰</span><span class="sxs-lookup"><span data-stu-id="1a787-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="1a787-106">設定之後，重新啟動 Azure Multi-Factor Authentication，「終端機服務」才會生效。</span><span class="sxs-lookup"><span data-stu-id="1a787-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="1a787-107">如果已核取 [需要進行 Azure Multi-Factor Authentication 使用者比對]，但您不在使用者清單中，則重新開機之後，您將無法登入機器。</span><span class="sxs-lookup"><span data-stu-id="1a787-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="1a787-108">信任的 IP 取決於應用程式是否可以提供用於驗證的用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="1a787-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="1a787-109">目前僅支援終端機服務。</span><span class="sxs-lookup"><span data-stu-id="1a787-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="1a787-110">在 Windows Server 2012 R2 上，不支援這項功能來保護終端機服務。</span><span class="sxs-lookup"><span data-stu-id="1a787-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="1a787-111">若要使用 Windows 驗證來保護應用程式，請使用下列程序。</span><span class="sxs-lookup"><span data-stu-id="1a787-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="1a787-112">在 Azure Multi-Factor Authentication Server 中，按一下 [Windows 驗證] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1a787-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="1a787-113">![Windows 驗證](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="1a787-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="1a787-114">核取 [啟用 Windows 驗證] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="1a787-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="1a787-115">預設不核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="1a787-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="1a787-116">[應用程式] 索引標籤可讓系統管理員設定一或多個應用程式要經過 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="1a787-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="1a787-117">選取伺服器或應用程式 – 指定是否啟用伺服器/應用程式。</span><span class="sxs-lookup"><span data-stu-id="1a787-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="1a787-118">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1a787-118">Click **OK**.</span></span>
5. <span data-ttu-id="1a787-119">按一下 [新增...]</span><span class="sxs-lookup"><span data-stu-id="1a787-119">Click **Add…**</span></span>
6. <span data-ttu-id="1a787-120">[信任的 IP] 索引標籤可讓您針對來自特定 IP 的 Windows 工作階段，略過 Azure Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="1a787-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="1a787-121">例如，如果員工從辦公室和家裡使用應用程式，您可能決定當他們在辦公室時不要響起 Azure Multi-Factor Authentication 的電話。</span><span class="sxs-lookup"><span data-stu-id="1a787-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="1a787-122">為此，您可以將辦公室子網路指定為信任的 IP 項目。</span><span class="sxs-lookup"><span data-stu-id="1a787-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="1a787-123">按一下 [新增...]</span><span class="sxs-lookup"><span data-stu-id="1a787-123">Click **Add…**</span></span>
8. <span data-ttu-id="1a787-124">如果您想要跳過單一 IP 位址，請選取 [單一 IP]。</span><span class="sxs-lookup"><span data-stu-id="1a787-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="1a787-125">如果您想要跳過整個 IP 範圍，請選取 [IP 範圍]。</span><span class="sxs-lookup"><span data-stu-id="1a787-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="1a787-126">範例：10.63.193.1-10.63.193.100。</span><span class="sxs-lookup"><span data-stu-id="1a787-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="1a787-127">如果您想要使用子網路標記法指定 IP 範圍，請選取 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="1a787-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="1a787-128">輸入子網路的起始 IP，並從下拉式清單中挑選適當的網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="1a787-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="1a787-129">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1a787-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a787-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1a787-130">Next steps</span></span>

- [<span data-ttu-id="1a787-131">設定 Azure MFA Server 的協力廠商 VPN 應用裝置</span><span class="sxs-lookup"><span data-stu-id="1a787-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="1a787-132">利用 Azure MFA 的 NPS 擴充功能強化現有的驗證基礎結構驗證</span><span class="sxs-lookup"><span data-stu-id="1a787-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)

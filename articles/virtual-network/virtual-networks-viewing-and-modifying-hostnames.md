---
title: "檢視與修改主機名稱 | Microsoft Docs"
description: "如何檢視和變更 Azure 虛擬機器的主機名稱、Web 和背景工作角色以進行名稱解析"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 9a3a1e1b58dcb828e2d2d09c18f1aab6d46051aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="viewing-and-modifying-hostnames"></a><span data-ttu-id="5a41a-103">檢視與修改主機名稱</span><span class="sxs-lookup"><span data-stu-id="5a41a-103">Viewing and modifying hostnames</span></span>
<span data-ttu-id="5a41a-104">若要允許主機名稱參考您的角色執行個體，您必須在各個角色的服務組態檔中設定主機名稱的值。</span><span class="sxs-lookup"><span data-stu-id="5a41a-104">To allow your role instances to be referenced by host name, you must set the value for the host name in the service configuration file for each role.</span></span> <span data-ttu-id="5a41a-105">您可以將需要的主機名稱新增到 **Role** 項目的 **vmName** 屬性。</span><span class="sxs-lookup"><span data-stu-id="5a41a-105">You do that by adding the desired host name to the **vmName** attribute of the **Role** element.</span></span> <span data-ttu-id="5a41a-106">**vmName** 屬性的值會做為各個角色執行個體之主機名稱的基底。</span><span class="sxs-lookup"><span data-stu-id="5a41a-106">The value of the **vmName** attribute is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="5a41a-107">例如，如果 **vmName** 是 webrole 且有三個該角色的執行個體，執行個體的主機名稱將是 webrole0、webrole1 以及 webrole2。</span><span class="sxs-lookup"><span data-stu-id="5a41a-107">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span> <span data-ttu-id="5a41a-108">您不需要指定組態檔中虛擬機器的主機名稱，因為虛擬機器的主機名稱會根據虛擬機器名稱填入。</span><span class="sxs-lookup"><span data-stu-id="5a41a-108">You do not need to specify a host name for virtual machines in the configuration file, because the host name for a virtual machine is populated based on the virtual machine name.</span></span> <span data-ttu-id="5a41a-109">如需設定 Microsoft Azure 服務的詳細資訊，請參閱 [Azure 服務組態結構描述 (.cscfg 檔)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span><span class="sxs-lookup"><span data-stu-id="5a41a-109">For more information about configuring a Microsoft Azure service, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx)</span></span>

## <a name="viewing-hostnames"></a><span data-ttu-id="5a41a-110">檢視主機名稱</span><span class="sxs-lookup"><span data-stu-id="5a41a-110">Viewing hostnames</span></span>
<span data-ttu-id="5a41a-111">您可以使用下列任何工具，在雲端服務中檢視虛擬機器和角色執行個體的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-111">You can view the host names of virtual machines and role instances in a cloud service by using any of the tools below.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="5a41a-112">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5a41a-112">Azure Portal</span></span>
<span data-ttu-id="5a41a-113">您可以使用 [Azure 入口網站](http://portal.azure.com) 檢視虛擬機器概觀刀鋒視窗上虛擬機器的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-113">You can use the [Azure portal](http://portal.azure.com) to view the host names for virtual machines on the overview blade for a virtual machine.</span></span> <span data-ttu-id="5a41a-114">請記住，刀鋒視窗中顯示**名稱**和**主機名稱**的值。</span><span class="sxs-lookup"><span data-stu-id="5a41a-114">Keep in mind that the blade shows a value for **Name** and **Host Name**.</span></span> <span data-ttu-id="5a41a-115">雖然它們一開始都相同，但是變更主機名稱不會變更虛擬機器或角色執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-115">Although they are initially the same, changing the host name will not change the name of the virtual machine or role instance.</span></span>

<span data-ttu-id="5a41a-116">角色執行個體也能在 Azure 入口網站中檢視，但是當您列出雲端服務中的執行個體時不會顯示主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-116">Role instances can also be viewed in the Azure portal, but when you list the instances in a cloud service, the host name is not displayed.</span></span> <span data-ttu-id="5a41a-117">您將會看到各個執行個體的名稱，但是該名稱不代表主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-117">You will see a name for each instance, but that name does not represent the host name.</span></span>

### <a name="service-configuration-file"></a><span data-ttu-id="5a41a-118">服務組態檔</span><span class="sxs-lookup"><span data-stu-id="5a41a-118">Service configuration file</span></span>
<span data-ttu-id="5a41a-119">您可以從 Azure 入口網站中服務的 [設定] 刀鋒視窗，下載已部署服務的服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="5a41a-119">You can download the service configuration file for a deployed service from the **Configure** blade of the service in the Azure portal.</span></span> <span data-ttu-id="5a41a-120">然後您可以尋找 **Role name** 項目的**vmName** 屬性，查看主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-120">You can then look for the **vmName** attribute for the **Role name** element to see the host name.</span></span> <span data-ttu-id="5a41a-121">請記住，這個主機名稱是做為各個角色執行個體之主機名稱的基底。</span><span class="sxs-lookup"><span data-stu-id="5a41a-121">Keep in mind that this host name is used as a base for the host name of each role instance.</span></span> <span data-ttu-id="5a41a-122">例如，如果 **vmName** 是 webrole 且有三個該角色的執行個體，執行個體的主機名稱將是 webrole0、webrole1 以及 webrole2。</span><span class="sxs-lookup"><span data-stu-id="5a41a-122">For example, if **vmName** is *webrole* and there are three instances of that role, the host names of the instances will be *webrole0*, *webrole1*, and *webrole2*.</span></span>

### <a name="remote-desktop"></a><span data-ttu-id="5a41a-123">遠端桌面</span><span class="sxs-lookup"><span data-stu-id="5a41a-123">Remote Desktop</span></span>
<span data-ttu-id="5a41a-124">啟用您虛擬機器或角色執行個體的遠端桌面 (Windows)、Windows PowerShell 遠端執行功能 (Windows) 或 SSH (Linux 和 Windows) 連線之後，您可以利用多種方式檢視使用中遠端桌面連線的主機名稱：</span><span class="sxs-lookup"><span data-stu-id="5a41a-124">After you enable Remote Desktop (Windows), Windows PowerShell remoting (Windows), or SSH (Linux and Windows) connections to your virtual machines or role instances, you can view the host name from an active Remote Desktop connection in various ways:</span></span>

* <span data-ttu-id="5a41a-125">在命令提示字元或 SSH 終端機中輸入主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-125">Type hostname at the command prompt or SSH terminal.</span></span>
* <span data-ttu-id="5a41a-126">在命令提示字元中輸入 ipconfig /all (僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="5a41a-126">Type ipconfig /all at the command prompt (Windows only).</span></span>
* <span data-ttu-id="5a41a-127">在系統設定中檢視電腦名稱 (僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="5a41a-127">View the computer name in the system settings (Windows only).</span></span>

### <a name="azure-service-management-rest-api"></a><span data-ttu-id="5a41a-128">Azure 服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="5a41a-128">Azure Service Management REST API</span></span>
<span data-ttu-id="5a41a-129">從 REST 用戶端，請遵循下列指示：</span><span class="sxs-lookup"><span data-stu-id="5a41a-129">From a REST client, follow these instructions:</span></span>

1. <span data-ttu-id="5a41a-130">確定您有連線到 Azure 入口網站的用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="5a41a-130">Ensure that you have a client certificate to connect to the Azure portal.</span></span> <span data-ttu-id="5a41a-131">若要取得用戶端憑證，請遵循[做法：下載與匯入發行設定與訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="5a41a-131">To obtain a client certificate, follow the steps presented in [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span> 
2. <span data-ttu-id="5a41a-132">設定名稱為 x-ms-version，值為 2013-11-01 的標頭項目。</span><span class="sxs-lookup"><span data-stu-id="5a41a-132">Set a header entry named x-ms-version with a value of 2013-11-01.</span></span>
3. <span data-ttu-id="5a41a-133">傳送下列格式的要求：https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span><span class="sxs-lookup"><span data-stu-id="5a41a-133">Send a request in the following format: https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<service-name\>?embed-detail=true</span></span>
4. <span data-ttu-id="5a41a-134">尋找各個 **RoleInstance** 項目的 **HostName** 項目。</span><span class="sxs-lookup"><span data-stu-id="5a41a-134">Look for the **HostName** element for each **RoleInstance** element.</span></span>

> [!WARNING]
> <span data-ttu-id="5a41a-135">您也可以透過檢查 **InternalDnsSuffix** 項目、從遠端桌面工作階段中的命令提示字元執行 ipconfig /all (Windows)，或從 SSH 終端機執行 cat /etc/resolv.conf (Linux)，檢視 REST 呼叫回應中您雲端服務的內部網域尾碼。</span><span class="sxs-lookup"><span data-stu-id="5a41a-135">You can also view the internal domain suffix for your cloud service from the REST call response by checking the **InternalDnsSuffix** element, or by running ipconfig /all from a command prompt in a Remote Desktop session (Windows), or by running cat /etc/resolv.conf from an SSH terminal (Linux).</span></span>
> 
> 

## <a name="modifying-a-hostname"></a><span data-ttu-id="5a41a-136">修改主機名稱</span><span class="sxs-lookup"><span data-stu-id="5a41a-136">Modifying a hostname</span></span>
<span data-ttu-id="5a41a-137">您可以透過上傳已修改的服務組態檔，或是從遠端桌面工作階段重新命名電腦，來修改任何虛擬機器或角色執行個體的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5a41a-137">You can modify the host name for any virtual machine or role instance by uploading a modified service configuration file, or by renaming the computer from a Remote Desktop session.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a41a-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a41a-138">Next steps</span></span>
[<span data-ttu-id="5a41a-139">名稱解析 (DNS)</span><span class="sxs-lookup"><span data-stu-id="5a41a-139">Name Resolution (DNS)</span></span>](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[<span data-ttu-id="5a41a-140">Azure 服務組態結構描述 (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="5a41a-140">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[<span data-ttu-id="5a41a-141">Azure 虛擬網路組態結構描述</span><span class="sxs-lookup"><span data-stu-id="5a41a-141">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="5a41a-142">使用網路組態檔指定 DNS 設定</span><span class="sxs-lookup"><span data-stu-id="5a41a-142">Specify DNS settings using network configuration files</span></span>](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)


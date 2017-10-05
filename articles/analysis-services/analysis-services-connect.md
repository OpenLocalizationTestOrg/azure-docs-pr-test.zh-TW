---
title: "連接到 Azure Analysis Services | Microsoft Docs"
description: "了解如何在 Azure 連線至 Analysis Services 伺服器並從該伺服器中取得資料。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="e58bd-103">連接到 Azure Analysis Services 伺服器</span><span class="sxs-lookup"><span data-stu-id="e58bd-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="e58bd-104">本文說明如何使用資料模型化和管理應用程式 (例如 SQL Server Management Studio (SSMS) 或 SQL Server Data Tools (SSDT)) 來連接到伺服器。</span><span class="sxs-lookup"><span data-stu-id="e58bd-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="e58bd-105">或是使用用戶端報表應用程式，例如 Microsoft Excel、Power BI Desktop 或自訂應用程式。</span><span class="sxs-lookup"><span data-stu-id="e58bd-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="e58bd-106">連到 Azure Analysis Services 的連線會使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="e58bd-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="e58bd-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e58bd-107">Client libraries</span></span>
[<span data-ttu-id="e58bd-108">取得最新的用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="e58bd-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="e58bd-109">所有連到伺服器的連線 (不論是哪一種類型) 都需要已更新的 AMO、ADOMD.NET 及 OLEDB 用戶端程式庫，才能連接到 Analysis Services 伺服器並與其銜接。</span><span class="sxs-lookup"><span data-stu-id="e58bd-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="e58bd-110">針對 SSMS、SSDT、Excel 2016 及 Power BI，最新的用戶端程式庫會隨著每月的發行版本一起安裝或更新。</span><span class="sxs-lookup"><span data-stu-id="e58bd-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="e58bd-111">不過，在某些情況下，應用程式的版本可能不會是最新的。</span><span class="sxs-lookup"><span data-stu-id="e58bd-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="e58bd-112">例如，當原則延遲更新，或 Office 365 更新是在「順延通道」上時。</span><span class="sxs-lookup"><span data-stu-id="e58bd-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="e58bd-113">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="e58bd-113">Server name</span></span>

<span data-ttu-id="e58bd-114">當您在 Azure 中建立 Analysis Services 伺服器時，您可以指定唯一的名稱和要建立伺服器的區域。</span><span class="sxs-lookup"><span data-stu-id="e58bd-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="e58bd-115">在連線中指定伺服器名稱時，伺服器命名配置為：</span><span class="sxs-lookup"><span data-stu-id="e58bd-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="e58bd-116">其中 protocol 是字串 **asazure**，region 是伺服器建立位置的 Uri (例如 westus.asazure.windows.net)，而 servername 則是該區域內您唯一伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="e58bd-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="e58bd-117">取得伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="e58bd-117">Get the server name</span></span>
<span data-ttu-id="e58bd-118">在 [Azure 入口網站] > 伺服器 > [概觀]  >  [伺服器名稱] 中，複製整個伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="e58bd-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="e58bd-119">如果您組織中的其他使用者也會連線到這部伺服器，您可以將此伺服器名稱告訴他們。</span><span class="sxs-lookup"><span data-stu-id="e58bd-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="e58bd-120">指定伺服器名稱時，必須使用完整路徑。</span><span class="sxs-lookup"><span data-stu-id="e58bd-120">When specifying a server name, the entire path must be used.</span></span>

![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="e58bd-122">Connection string</span><span class="sxs-lookup"><span data-stu-id="e58bd-122">Connection string</span></span>

<span data-ttu-id="e58bd-123">使用表格式物件模型連線至 Azure Analysis Services 時，請使用下列連接字串格式：</span><span class="sxs-lookup"><span data-stu-id="e58bd-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="e58bd-124">整合型 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="e58bd-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="e58bd-125">整合型驗證會挑選 Azure Active Directory 認證快取 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="e58bd-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="e58bd-126">如果沒有，則會顯示 Azure 登入視窗。</span><span class="sxs-lookup"><span data-stu-id="e58bd-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="e58bd-127">以使用者名稱與密碼進行的 Azure Active Directory 驗證</span><span class="sxs-lookup"><span data-stu-id="e58bd-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="e58bd-128">Windows 驗證 (整合式安全性)</span><span class="sxs-lookup"><span data-stu-id="e58bd-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="e58bd-129">請使用執行目前程序的 Windows 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e58bd-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="e58bd-130">使用 .odc 檔案進行連接</span><span class="sxs-lookup"><span data-stu-id="e58bd-130">Connect using an .odc file</span></span>
<span data-ttu-id="e58bd-131">在使用舊版 Excel 的情況下，使用者可以使用「Office 資料連線」(.odc) 檔案來連接到 Azure Analysis Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e58bd-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="e58bd-132">若要深入了解，請參閱[建立 Office 資料連線 (.odc) 檔案](analysis-services-odc.md)。</span><span class="sxs-lookup"><span data-stu-id="e58bd-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e58bd-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e58bd-133">Next steps</span></span>
<span data-ttu-id="e58bd-134">[使用 Excel 進行連接](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="e58bd-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="e58bd-135">[使用 Power BI 進行連接](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="e58bd-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="e58bd-136">管理您的伺服器</span><span class="sxs-lookup"><span data-stu-id="e58bd-136">Manage your server</span></span>](analysis-services-manage.md)   


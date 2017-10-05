---
title: "變更 Azure 微服務中的 FabricTransport 設定 | Microsoft Docs"
description: "深入了解設定 Azure Service Fabric 動作項目通訊設定。"
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="4b884-103">設定 Reliable Actors 的 FabricTransport 設定</span><span class="sxs-lookup"><span data-stu-id="4b884-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="4b884-104">您可以進行的設定包括︰</span><span class="sxs-lookup"><span data-stu-id="4b884-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="4b884-105">C#：[FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="4b884-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="4b884-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="4b884-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="4b884-107">您可以下列方式修改 FabricTransport 的預設設定。</span><span class="sxs-lookup"><span data-stu-id="4b884-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="4b884-108">組件屬性</span><span class="sxs-lookup"><span data-stu-id="4b884-108">Assembly attribute</span></span>

<span data-ttu-id="4b884-109">[FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) 屬性需要在動作項目用戶端和動作項目服務組件上套用。</span><span class="sxs-lookup"><span data-stu-id="4b884-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="4b884-110">下列範例顯示如何變更 FabricTransport OperationTimeout 設定的預設值：</span><span class="sxs-lookup"><span data-stu-id="4b884-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="4b884-111">第二個範例會變更 FabricTransport MaxMessageSize 和 OperationTimeoutInSeconds 的預設值。</span><span class="sxs-lookup"><span data-stu-id="4b884-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="4b884-112">組態封裝</span><span class="sxs-lookup"><span data-stu-id="4b884-112">Config package</span></span>

<span data-ttu-id="4b884-113">您可以使用[組態封裝](service-fabric-application-model.md)修改預設組態。</span><span class="sxs-lookup"><span data-stu-id="4b884-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="4b884-114">設定動作項目服務的 FabricTransport 設定</span><span class="sxs-lookup"><span data-stu-id="4b884-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="4b884-115">在 settings.xml 檔案中新增 TransportSettings 區段。</span><span class="sxs-lookup"><span data-stu-id="4b884-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="4b884-116">根據預設，動作項目程式碼會尋找 SectionName 做為「&lt;ActorName&gt;TransportSettings」。</span><span class="sxs-lookup"><span data-stu-id="4b884-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="4b884-117">如果找不到，它會以「TransportSettings」檢查 SectionName 。</span><span class="sxs-lookup"><span data-stu-id="4b884-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="4b884-118">設定動作項目用戶端組件的 FabricTransport 設定</span><span class="sxs-lookup"><span data-stu-id="4b884-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="4b884-119">如果用戶端未當作服務一部分執行，則您可以在 client .exe 檔案存在的同一位置中建立「&lt;Client Exe Name&gt;.settings.xml」檔案。</span><span class="sxs-lookup"><span data-stu-id="4b884-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="4b884-120">然後在該檔案中新增 TransportSettings 區段。</span><span class="sxs-lookup"><span data-stu-id="4b884-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="4b884-121">SectionName 應為「TransportSettings」。</span><span class="sxs-lookup"><span data-stu-id="4b884-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="4b884-122">使用第二個憑證來設定安全動作服務/用戶端的 FabricTransport 設定。</span><span class="sxs-lookup"><span data-stu-id="4b884-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="4b884-123">您可以新增參數 CertificateFindValuebySecondary，將次要憑證資訊加以新增。</span><span class="sxs-lookup"><span data-stu-id="4b884-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="4b884-124">以下是接聽程式 TransportSettings 的範例。</span><span class="sxs-lookup"><span data-stu-id="4b884-124">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="4b884-125">以下是用戶端 TransportSettings 的範例。</span><span class="sxs-lookup"><span data-stu-id="4b884-125">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="4b884-126">使用主體名稱來設定安全動作服務/用戶端的 FabricTransport 設定。</span><span class="sxs-lookup"><span data-stu-id="4b884-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="4b884-127">使用者必須提供 findType 作為 FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames 值。</span><span class="sxs-lookup"><span data-stu-id="4b884-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="4b884-128">以下是接聽程式 TransportSettings 的範例。</span><span class="sxs-lookup"><span data-stu-id="4b884-128">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="4b884-129">以下是用戶端 TransportSettings 的範例。</span><span class="sxs-lookup"><span data-stu-id="4b884-129">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```

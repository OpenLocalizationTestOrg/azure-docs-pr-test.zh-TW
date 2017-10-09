<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="d6322-101">準備更新</span><span class="sxs-lookup"><span data-stu-id="d6322-101">Preparing for updates</span></span>
<span data-ttu-id="d6322-102">您將需要 tooperform hello 掃描並套用 hello 更新之前，下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d6322-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="d6322-103">取得 hello 裝置資料的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="d6322-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="d6322-104">請確定您的控制器固定 Ip 可路由傳送，且可以連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="d6322-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="d6322-105">這些固定 Ip 會是使用的 tooservice 更新 tooyour 裝置。</span><span class="sxs-lookup"><span data-stu-id="d6322-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="d6322-106">您可以執行 hello hello 裝置 hello Windows PowerShell 介面中的下列每個控制站上的指令程式來測試：</span><span class="sxs-lookup"><span data-stu-id="d6322-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="d6322-107">**測試連線時固定的 Ip 可連線網際網路 toohello 範例輸出**</span><span class="sxs-lookup"><span data-stu-id="d6322-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="d6322-108">您已成功完成這些手動前檢查之後，您可以繼續 tooscan 並安裝 hello 更新。</span><span class="sxs-lookup"><span data-stu-id="d6322-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>


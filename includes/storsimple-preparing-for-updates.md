<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>準備更新
您將需要 tooperform hello 掃描並套用 hello 更新之前，下列步驟：

1. 取得 hello 裝置資料的雲端快照。
2. 請確定您的控制器固定 Ip 可路由傳送，且可以連接 toohello 網際網路。 這些固定 Ip 會是使用的 tooservice 更新 tooyour 裝置。 您可以執行 hello hello 裝置 hello Windows PowerShell 介面中的下列每個控制站上的指令程式來測試：
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **測試連線時固定的 Ip 可連線網際網路 toohello 範例輸出**

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

您已成功完成這些手動前檢查之後，您可以繼續 tooscan 並安裝 hello 更新。


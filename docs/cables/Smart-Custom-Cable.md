# Smart-Custom Cable for SmartUPSes

You do not have this cable unless you built it yourself. The Smart-Custom cable is not an APC product.

## SMART-CUSTOM CABLE

| Signal | Computer (DB9F) | UPS (DB9M) | Function      |
| :----- | :-------------- | :--------- | :------------ |
| RxD    | 2               | 2          | TxD (Send)    |
| TxD    | 3               | 1          | RxD (Receive) |
| GND    | 5               | 9          | Ground        |

```mermaid
graph LR
    subgraph Computer [Computer DB9F]
        PC_RxD[Pin 2: RxD]
        PC_TxD[Pin 3: TxD]
        PC_GND[Pin 5: Ground]
    end

    subgraph UPS [UPS DB9M]
        UPS_TxD[Pin 2: TxD]
        UPS_RxD[Pin 1: RxD]
        UPS_GND[Pin 9: Ground]
    end

    PC_RxD --- UPS_TxD
    PC_TxD --- UPS_RxD
    PC_GND --- UPS_GND
```

If you have an OS that requires DCD or RTS to be set before you can receive input, you might try building the standard APC Smart 940-0024C cable (see "[940-0024C Cable Wiring](940-0024C.md)").

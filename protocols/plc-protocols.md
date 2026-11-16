
# EM300 Supported PLC Protocols

The IOTRouter EM300 Industrial Edge Controller supports communication with PLCs from major industrial automation manufacturers through Ethernet and serial interfaces.

The supported PLC integrations are organized by brand, communication protocol, interface, and model.

**Compatibility Note**

Representative PLC models from each brand have been selected for testing. Other supported model information is based on official manufacturer documentation.

The EM300 also supports standard Modbus RTU/TCP communication, which is widely used by mainstream PLCs, including HollySys, Haiwell, Yokogawa, Runpower, and others.

## 1. Siemens

Siemens PLCs primarily use the S7 protocol for communication.

| Protocol | Interface | Supported Models |
|---|---|---|
| S7 | Ethernet | S7-200 SMART, S7-200, S7-300, S7-400, S7-1200, S7-1500 |
| PPI | Serial Port | S7-200 |

**Recommendation:** S7 communication is recommended for Siemens PLC integration.

## 2. Mitsubishi MELSEC

Mitsubishi PLCs mainly use the MC protocol.

| Protocol | Interface | Supported Models |
|---|---|---|
| EtherNet/IP | Ethernet | FX5-ENET/IP, RJ71EIP91, QJ71EIP71 |
| MC-1E / MC-3E | Ethernet | FX5, RJ71EN71, RnENCPU, LJ71E71, QJ71E71, QnUCPU, FX3 |
| Modbus TCP | Ethernet | FX5, RJ71EN71, RnENCPU, LJ71E71, QJ71E71 |
| MC-3C | Serial Port | FX5, RJ71C24, LJ71C24, QJ71C24 |
| Modbus RTU | Serial Port | FX5, RJ71C24, LJ71C24, QJ71C24, FX3 |
| FxLinks | Serial Port | FX3, FX2, FX1, FX0 |
| FxSerial | Serial Port | FX3, FX2, FX1, FX0 |

## 3. Omron

Omron PLCs mainly use the FINS protocol.

| Protocol | Interface | Supported Models |
|---|---|---|
| EtherNet/IP | Ethernet | NX7, NX1, NX1P, NJ, CJ1W-EIP21 |
| FINS | Ethernet | CP, CS, CJ, CV |
| HostLink | Serial Port | CP, CS, CJ, CV, C |

## 4. LS Electric

LS PLCs mainly use FEnet and Cnet protocols.

| Protocol | Interface | Supported Models |
|---|---|---|
| XGB FEnet | Ethernet | XGB (XBC/XEC U, XBL-EMTA) |
| XGK FEnet | Ethernet | XGT (XGL-EFMT, XGL-EFMF, XGL-EH5T) |
| XGB Cnet | Serial Port | XGB (XBC/XEC U, XBL-C21A, XBL-C41A) |
| XGK Cnet | Serial Port | XGT (XGL-CH2A, XGL-C21A, XGL-C41A) |

## 5. Allen-Bradley (Rockwell Automation)

Rockwell PLCs mainly use CIP and DF1 protocols.

| Protocol | Interface | Supported Models |
|---|---|---|
| EtherNet/IP | Ethernet | ControlLogix, CompactLogix, Micro800 (820, 850, 870) |
| DF1 | Serial Port | ControlLogix and CompactLogix (5069-SERIAL module); SLC 500, 5/03, 5/04, 5/05; MicroLogix 1000, 1100, 1200, 1500; Micro800 (820, 830, 850, 870) |

## 6. Beckhoff

| Protocol | Interface | Supported Models |
|---|---|---|
| ADS | Ethernet | CX Series, TwinCAT 2, TwinCAT 3 |

## 7. Inovance

Inovance PLCs mainly use Modbus communication.

| Protocol | Interface | Supported Models |
|---|---|---|
| Modbus TCP | Ethernet | AC, AM, H5U, H3U |
| Modbus RTU | Serial Port | AC, AM, H5U, H3U, H1U |

## 8. Keyence

Keyence PLCs mainly use the KV protocol.

| Protocol | Interface | Supported Models |
|---|---|---|
| MC-3E | Ethernet | KV-8000, KV-7000, KV-5500, KV-5000, KV-EP21V, KV-LE21V, KV-LE20V, KV-LE20A |
| KV | Ethernet | KV Series |
| KV | Serial Port | KV-7300, KV-3000, KV-1000, KV-700, KV Nano, KV-L21V, KV-L20V |

## 9. Panasonic

Panasonic PLCs mainly use the Mewtocol protocol.

| Protocol | Interface | Supported Models |
|---|---|---|
| MC-3E | Ethernet | FP7, FP0H, FP-XH |
| Mewtocol | Ethernet | FP7, FP0H, FP-XH |
| Mewtocol | Serial Port | FP7, FP0H, FP-XH, FP-X0, FP0R |

## 10. Delta

Delta PLCs mainly use Modbus communication.

| Protocol | Interface | Supported Models |
|---|---|---|
| Modbus TCP | Ethernet | AH, AS, AX-3, DVP (built-in Ethernet) |
| Modbus RTU | Serial Port | AH, AS, AX-3, DVP |

## 11. XinJE

| Protocol | Interface | Supported Models |
|---|---|---|
| Modbus TCP | Ethernet | CCSD, XA, XS, XG, XL |
| Modbus RTU | Serial Port | CCSD, XA, XS, XG, XL, XC, XD |

## 12. MegMeet

| Protocol | Interface | Supported Models |
|---|---|---|
| Modbus TCP | Ethernet | MC5100, MC280, MC200, MC100, MC80 |
| Modbus RTU | Serial Port | MC5100, MC280, MC200, MC100, MC80 |

## 13. Yaskawa

| Protocol | Interface | Supported Models |
|---|---|---|
| MEMOBUS | Ethernet | GL120/130, GL60, MP3000, MP2300, Z1000 |

## 14. Fatek

| Protocol | Interface | Supported Models |
|---|---|---|
| Fatek | Serial Port | FBs Series |

## 15. Vigor

| Protocol | Interface | Supported Models |
|---|---|---|
| VS | Serial Port | VS Series |

## 16. Fuji

| Protocol | Interface | Supported Models |
|---|---|---|
| SPH | Ethernet | SPH Series |
| SPB | Serial Port | SPB Series |

---

## Communication Interfaces

The EM300 supports PLC communication through Ethernet and serial interfaces.

Supported communication protocols include:

- Ethernet-based protocols: S7, MC Protocol, EtherNet/IP, FINS, ADS, Modbus TCP, and others.
- Serial-based protocols: PPI, HostLink, DF1, Modbus RTU, Mewtocol, and others.

For model-specific compatibility and communication configuration, refer to the corresponding protocol documentation.

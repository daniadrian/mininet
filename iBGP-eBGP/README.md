# BGP Routing Implementation

## Project Overview
This project implements BGP (Border Gateway Protocol) routing in a Mininet environment based on a specified network topology consisting of three Autonomous Systems (AS).

## Network Topology

![Screenshot 2024-10-24 155734](https://github.com/user-attachments/assets/0d46ec14-d171-464c-b198-5a7fd362ec72)

*The network consists of three Autonomous Systems interconnected through eBGP, with internal routers using iBGP and OSPF.*

### Autonomous System Details

#### AS 100
- **Routers**: R11, R12, R13, R14
- **Devices**:
  - Client: C11
  - Switch: S11 (connects C11 to R11)
- **Internal Structure**:
  - Forms a full mesh topology between all routers
  - R14 serves as the edge router for eBGP connection
- **Connections**:
  - R14 connects to R22 (AS200) via eBGP
  - All internal routers connected via iBGP
  - OSPF running internally

#### AS 200
- **Routers**: R21, R22, R23, R24
- **Devices**:
  - Client: C22
  - Switch: S2 (connects C22 to R21)
- **Internal Structure**:
  - Forms a full mesh topology between all routers
  - R22 and R23 serve as edge routers
- **Connections**:
  - R22 connects to R14 (AS100) via eBGP
  - R23 connects to R34 (AS300) via eBGP
  - All internal routers connected via iBGP
  - OSPF running internally

#### AS 300
- **Routers**: R31, R32, R33, R34
- **Devices**:
  - Client: C33
  - Switch: S33 (connects C33 to R33)
- **Internal Structure**:
  - Forms a full mesh topology between all routers
  - R34 serves as the edge router
- **Connections**:
  - R34 connects to R23 (AS200) via eBGP
  - All internal routers connected via iBGP
  - OSPF running internally

### Protocol Implementation
1. **External BGP (eBGP)**:
   - Connection between AS100 and AS200: R14 - R22
   - Connection between AS200 and AS300: R23 - R34
   - Shown as red dashed lines in the topology

2. **Internal BGP (iBGP)**:
   - Full mesh iBGP connections within each AS
   - Shown as black dashed lines in the topology

3. **OSPF**:
   - Running within each AS
   - Used for internal routing

### Client Connectivity
- C11: Connected to AS100 through switch S11 and router R11
- C22: Connected to AS200 through switch S2 and router R21
- C33: Connected to AS300 through switch S33 and router R33

## Project Requirements
1. Implement the complete network topology in Mininet environment
2. Configure all routing protocols:
   - eBGP for inter-AS communication
   - iBGP for intra-AS routing
   - OSPF for internal routing within each AS
3. Ensure proper connectivity between all clients

# Testing and Results
```
show ip prefix-list
```
![Screenshot 2024-12-15 191142](https://github.com/user-attachments/assets/7c996ad2-c0f6-4c40-9a76-8a0583d790a4)

Daftar prefix-list yang telah dikonfigurasi di router, termasuk nama, urutan, aturan yang digunakan, dan jumlah entri dalam prefix-list.

```
C11 traceroute C33
```
![image](https://github.com/user-attachments/assets/a35968b5-655c-41da-9758-47a238edf8fd)

```
show ip bgp neighbors 10.10.1.2 received-routes
```
![image](https://github.com/user-attachments/assets/c780b2fb-60e8-4c91-99ab-5720747daff7)

`show ip bgp neighbors 10.10.1.2 received-routes` menampilkan semua rute yang diterima dari neighbor BGP 10.10.1.2, termasuk informasi Next Hop, AS-Path, dan status rute.

## Licencse
This project is licensed under the Creative Commons Legal Code CC0 1.0 Universal. See the [LICENSE](LICENSE) file for details.

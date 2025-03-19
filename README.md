# 5G_ORAN
Developing 5G Private Network
# **5G ORAN Development using USRP N321 and srsRAN**

## **Project Overview**

This project focuses on the **design and development of a 5G ORAN-based Private Network** using the **USRP N321 Software Defined Radio (SDR)** hardware and the **srsRAN 5G** open-source software suite. The objective is to implement a scalable and reliable **5G private network** while also integrating **srsRAN 4G and OpenAirInterface (OAI)** for enhanced flexibility. The setup leverages **ZeroMQ** for efficient communication, supports multiple UEs, and incorporates **Grafana for real-time performance monitoring**.

## **Table of Contents**
- [Objective and Goals](#objective-and-goals)
- [Project Team](#project-team)
- [Technologies Used](#technologies-used)
- [Architecture](#architecture)
- [Installation and Setup](#installation-and-setup)
- [Testing](#testing)
- [Future Work](#future-work)
- [References](#references)

---

## **Objective and Goals**

### **Objective:**
To design, implement, and evaluate a **5G ORAN-based private network** using the **USRP N321**, integrating **srsRAN 5G, srsRAN 4G, and OpenAirInterface (OAI)**. This project aims to provide a **flexible and scalable** network architecture, ensuring **high reliability, low latency, and efficient resource utilization**.

### **Goals:**
- **Deploy a 5G private network** using USRP N321 and integrate **srsRAN 5G, srsRAN 4G, and OAI**.
- Implement **ZeroMQ for efficient communication** between network components.
- **Support and evaluate single and multiple UEs**, ensuring robust connectivity and performance.
- Utilize **Grafana for real-time monitoring**, analyzing **throughput, latency, and reliability**.

---

## **Project Team**

- **P. Prudvi Reddy** (BU21EECE0100361)
- **MC Mokshith** (BU21EECE0100391)
- **B. Gopal** (BU21EECE0100377)

**Mentor:**  
Dr. T Nagarjuna, Assistant Professor  
**Project In-charge:**  
Dr. Pankaj Kandhway

---

## **Technologies Used**

- **Software:**
  - srsRAN 5G & 4G (for 5G/4G network setup and management)
  - OpenAirInterface (OAI) for additional core network functionalities
  - ZeroMQ (for low-latency inter-component communication)
  - Grafana (for real-time monitoring and visualization)

- **Hardware:**
  - USRP N321 (Software Defined Radio for gNB/eNB deployment)
  
- **Operating System:**
  - Linux (Ubuntu for srsRAN & OAI deployment)

- **Programming & Configuration Tools:**
  - CMake, Bash scripting for setup automation
  - `srsran_5g_install_configs.sh` (for configuration setup)
  - `gedit` for configuration file editing

---

## **Architecture**

### **Structural Architecture**
- **gNB/eNodeB**: Handles radio communication with mobile devices.
- **Core Network (5GC & EPC)**:
  - **MME** (Mobility Management Entity): Handles authentication and session management.
  - **HSS** (Home Subscriber Server): Stores user profiles and authentication data.
  - **SGW & PGW**: Handles routing and connectivity between the LTE/5G network and external networks.
  - **Distributed Unit (DU)**: Handles Layer 1 (PHY) and Layer 2 (MAC, RLC) processing.
  - **Central Unit (CU)**: Manages higher-layer functions, mobility, and security.

### **Behavioral Architecture**
- **gNB/eNodeB processes LTE/5G signals using SDR**
- **CU-DU split architecture optimizes performance**
- **ZeroMQ ensures efficient data exchange**

---

## **Installation and Setup**

### **Install srsRAN and Dependencies**
```bash
git clone https://github.com/srsran/srsRAN_5G.git
cd srsRAN_5G/build
make clean
cmake ..
make
sudo make install
sudo srsran_5g_install_configs.sh <user/service>
```

### **Configure gNB and Core Network**
1. **Edit the gNB configuration file:**
    ```bash
    sudo gedit /root/.config/srsran/gnb.conf
    ```
    ```ini
    mcc = 001
    mnc = 01
    tac = 7
    gnb_id = 19
    ```
2. **Configure EPC/5GC:**
    ```bash
    sudo gedit /root/.config/srsran/epc.conf
    ```
3. **Add UE details in user database:**
    ```bash
    sudo gedit /root/.config/srsran/user_db.csv
    ```
    ```csv
    IMSI,K,OPC,AMF
    001010000000001,465B5CE8B199B49FAA5F0A2EE238A6BC,E8ED289DEBA952E4283B54E88E6183CA,8000
    ```

### **Start gNB and EPC/5GC**
```bash
sudo srsepc
sudo srsenb
```

---

## **Testing and Performance Analysis**

### **Test Cases**
1. **gNB Deployment Test:** Verify proper configuration and operation.
2. **UE Connectivity Test:** Ensure UEs can attach to the network.
3. **APN Configuration Test:** Validate network access via configured APN.
4. **Performance Monitoring:** Utilize **Grafana** to analyze key metrics (throughput, latency, reliability).

---

## **Future Work**

1. **DPDK Integration:** Optimize packet processing efficiency.
2. **Kubernetes Deployment:** Implement containerized srsRAN 5G for scalability.
3. **Voice Over LTE (VoLTE) & IMS Integration:** Enable voice call functionality.
4. **Enhancing Security Features:** Improve encryption and authentication mechanisms.

---

## **References**
- srsRAN 5G: [https://github.com/srsran/srsRAN](https://github.com/srsran/srsRAN)
- Ettus Research USRP N321: [https://www.ettus.com/all-products/usrp-n321/](https://www.ettus.com/all-products/usrp-n321/)
- Open5GS: [https://github.com/open5gs/open5gs](https://github.com/open5gs/open5gs)
- Grafana: [https://github.com/grafana/grafana](https://github.com/grafana/grafana)

---


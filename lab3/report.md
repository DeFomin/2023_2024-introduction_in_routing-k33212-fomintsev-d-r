University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Fomintsev Denis Ruslanovich  
Lab: Lab3  
Date of create: 08.12.2023  
Date of finished: 10.12.2023  

## Лабораторная работа №3 "Эмуляция распределенной корпоративной сети связи, настройка OSPF и MPLS, организация первого EoMPLS"

### Оглавление
- [Описание](#section1)
- [Цель работы](#section2)
- [Ход работы](#section4)
  - [Схема сети](#section4.1)
  - [PC1 и Router SPB](#section4.2)
  - [Routers HKI; MSK; LBN; LND](#section4.3)
  - [SGI_Prism и Router NYC](#section4.4)
  - [Проверка](#section4.5)
- [Вывод](#section4.6)

## <a name="section1">Описание</a>

* **OSPF (Open Shortest Path First):**  
OSPF - это протокол динамической маршрутизации, разработанный для использования в IP-сетях. Он основан на алгоритме Dijkstra и предназначен для поиска кратчайших путей к сетевым узлам.

Основные характеристики OSPF включают:  

1. Link-State Database (LSDB): OSPF поддерживает базу данных состояний связей, которая содержит информацию о всех маршрутизаторах в сети и их связях.

2. Areas: Сеть OSPF обычно разделяется на области (areas) для более эффективного управления трафиком и уменьшения объема информации в базе данных.

3. Hello Protocol: OSPF использует протокол Hello для обнаружения соседних маршрутизаторов и обмена информацией.

4. Dijkstra's SPF Algorithm: OSPF использует алгоритм SPF для вычисления кратчайших путей и построения маршрутных таблиц.


* **MPLS (Multiprotocol Label Switching):**  
MPLS - это технология коммутации пакетов, которая позволяет маршрутизаторам принимать решения на основе меток (labels), вместо использования IP-адресов. Основные компоненты MPLS включают:  

1. Label Switch Router (LSR): Маршрутизатор, способный коммутировать трафик на основе MPLS-меток.

2. Label Edge Router (LER): Маршрутизатор, который добавляет или удаляет метки MPLS при входе или выходе из MPLS-сети.

3. Label Distribution Protocol (LDP): Протокол, используемый для распределения меток между MPLS-маршрутизаторами.

* **EoMPLS (Ethernet over MPLS):**  
EoMPLS представляет собой механизм, который позволяет транспортировать Ethernet-фреймы через сеть MPLS. В основе EoMPLS лежит идея упаковки Ethernet-фреймов в MPLS-метки для их переноса через MPLS-сеть.  

Основные шаги для организации EoMPLS включают:  

1. Маршрутизаторы LER: На краю сети MPLS добавляются и удаляются MPLS-метки для фреймов Ethernet.

2. Label Mapping: LER использует LDP для обмена информацией о метках с соседними маршрутизаторами.

3. MPLS Tunneling: Ethernet-фреймы упаковываются в MPLS-метки и транспортируются через сеть MPLS.

**EoMPLS позволяет создавать виртуальные Ethernet-сегменты через MPLS-сеть, что полезно, например, для объединения удаленных локальных сетей в единую виртуальную сеть.**


Наша компания "RogaIKopita Games" с прошлой лабораторной работы выросла до серьезного игрового концерна, ещё немного и они выпустят свой ответ Genshin Impact - Allmoney Impact. И вот для этой задачи они купили небольшую, но очень старую студию "Old Games" из Нью Йорка, при поглощении выяснилось что у этой студии много наработок в области компьютерной графики и совет директоров "RogaIKopita Games" решил взять эти наработки на вооружение. К сожалению исходники лежат на сервере "SGI Prism", в Нью-Йоркском офисе никто им пользоваться не умеет, а из-за короновируса сотрудники офиса из Санкт-Петерубурга не могут добраться в Нью-Йорк, чтобы забрать данные из "SGI Prism". Ваша задача подключить Нью-Йоркский офис к общей IP/MPLS сети и организовать EoMPLS между "SGI Prism" и компьютером инженеров в Санк-Петербурге.

## <a name="section2">Цель работы</a>

Изучить протоколы OSPF и MPLS, механизмы организации EoMPLS.

## <a name="section4">Ход работы</a>

### <a name="section4.1">Схема сети</a>

Создаем файл сети, согласно схеме, представленной в лабораторной работе №3

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/385d2eca-8d38-4fc3-b609-c9b3635ce15e" width=900></p>

С помощью команды ```sudo containerlab graph -t mpls.yaml```:  

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/0418a209-5284-440c-9e8b-fa035abf2a69" width=900></p>

### <a name="section4.2">PC1 и Router SPB</a>

Для начала настроим наш PC1.

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/0c2bd950-6258-47ca-a4a6-7dbe0da6cd12" width=900></p>
<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/071312be-2335-4c21-ade3-0d57ca66fb7f" width=900></p>


Создаем интерфейсы EoMPLS_Bridge и Loopback (Lo0) на соответствующих узлах. Эти интерфейсы будут использоваться для установки MPLS-связей.  
* Виртуальный интерфейс Loopback может использоваться для установки уникального IP-адреса, который представляет устройство в сети.  
* EoMPLS_Bridge используется для транспорта Ethernet-трафика через MPLS-сеть. Он предоставляет механизм для создания виртуальных мостов между удаленными узлами с использованием MPLS  

Настроим VPLS (Virtual Private LAN Service) на интерфейсе EoMPLS_Bridge. В этой конфигурации укажим параметры, такие как MAC-адрес, максимальный размер передаваемого кадра (L2MTU) и адрес конечной точки удаленного узла. Это свяжет интерфейс с VPLS-службой и определит параметры, необходимые для обеспечения виртуальной приватной службы LAN.

mtu - максимальный размер передаваемого пакета (в байтах).  
l2mtu - максимальный размер передаваемого L2-кадра (в байтах).  
arp - включает (enabled) или отключает (disabled) ARP на этом интерфейсе. Он нужен для определения mac адреса устройства по ip адресу.  
remote-peer - IP-адрес удаленного узла.  

**VPLS - это технология, предназначенная для создания виртуальных локальных сетей через широкую сеть, такую как Интернет. Она обеспечивает расширение сети Ethernet через MPLS, создавая виртуальную сеть, которая кажется участникам, будто они подключены к одной общей Ethernet-сети.**

**MPLS может использоваться для установки туннелей и пересылки пакетов между удаленными сетевыми узлами. В случае VPLS, MPLS может использоваться для создания виртуальных соединений, объединяющих локальные Ethernet-сегменты на различных местах в единую виртуальную локальную сеть.**

**MPLS предоставляет инфраструктуру для установки виртуальных соединений, а VPLS использует эту инфраструктуру для создания виртуальных локальных сетей.**

**OSPF играет роль в определении маршрутов в IP-сетях, которые соединяют различные узлы MPLS и VPLS. OSPF может использоваться для обмена информацией о маршрутах между маршрутизаторами в сети MPLS, включая маршрутизаторы, обслуживающие VPLS.**


<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/200ac51f-cc1d-446a-9906-eb7dc720a3bb" width=900></p>


Опция ```cisco-style``` и ```cisco-style-id``` в команде ```/interface vpls add``` в MikroTik RouterOS предоставляют возможность использовать формат метки, схожий с тем, который принят в устройствах Cisco для VPLS.

Команда ```/routing ospf network add area=backbone``` в MikroTik RouterOS используется для добавления сетевого интерфейса в определенную зону OSPF area=backbone: Указывает, что сетевой интерфейс должен быть добавлен в OSPF-зону, которая называется "backbone" (главная зона OSPF с идентификатором 0.0.0.0). Зона OSPF (Area) - это логическая группа устройств OSPF внутри автономной системы (AS). OSPF разделяет сеть на зоны, и каждый маршрутизатор в зоне знает о всех маршрутах внутри этой зоны.  

Это необходимо для того, чтобы данный интерфейс стал частью OSPF-роутинга и маршрутизатор мог обмениваться информацией о маршрутах с другими маршрутизаторами в этой зоне  

### <a name="section4.3">Routers HKI; MSK; LBN; LND</a>

* **Настройка роутера HKI**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/07535bb2-2ff4-48e4-9744-c330cca599eb" width=900></p>

* **Настройка роутера MSK**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/7087c1ea-a27f-41c3-bf3a-fc633aefc760" width=900></p>

* **Настройка роутера LBN**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/d22155d5-f52f-4397-bf9c-5e099165d915" width=900></p>

* **Настройка роутера LND**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/fda1dac9-d523-441c-9031-fd3f693502f0" width=900></p>

### <a name="section4.4">SGI_Prism и Router NYC</a>

* **Настройка роутера NYC**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/c0771438-b8b7-4f7c-acbd-e3ce5076bb42" width=900></p>

* **Настройка SGI_Prism**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/8a7c9f03-5e3f-4888-a0d6-40fcc64a690f" width=900></p>

### <a name="section4.5">Проверка</a>

**Результат конфигурации MPLS**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/4e586a22-b1d9-46d0-bfd7-c1665e7acae6" width=900></p>

* L - ldp: Указывает, что некоторые записи связаны с протоколом LDP (Label Distribution Protocol).  
* T - traffic-eng: Относится к записям, связанным с механизмами Traffic Engineering (TE) MPLS.  

* OUT-LABELS: Выходные метки, которые указывают, какие метки будут использоваться для пересылки трафика к следующему узлу.
* DESTINATION: Адрес или сеть, для которой настроена метка.  
* INTERFACE: Интерфейс, через который отправляется трафик с соответствующей меткой.  

**Отслеживание маршрута от роутера NYC до роутера SPB**

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/80efe296-2547-4504-8448-61de5a29cfcb" width=900></p>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/b8077b1a-e47e-44d2-ab45-6d2c00443a31" width=900></p>



## <a name="section4.6">Вывод</a>

В ходе выполнения данной лабораторной работы мы на практике познакомились с протоколами OSPF, MPLS, EoMPLS и механизмами их организации.











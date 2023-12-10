University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Fomintsev Denis Ruslanovich  
Lab: Lab4  
Date of create: 09.12.2023  
Date of finished: 10.12.2023  

## Лабораторная работ №4 "Эмуляция распределенной корпоративной сети связи, настройка iBGP, организация L3VPN, VPLS"

### Оглавление
- [Описание](#section1)
- [Цель работы](#section2)
- [Ход работы](#section4)
  - [Построение схемы](#section4.1)
  - [](#section4.2)
  - [](#section4.3)
  - [](#section4.4)
- [Вывод](#section4.5)
 
## <a name="section1">Описание</a>

Компания "RogaIKopita Games" выпустила игру "Allmoney Impact", нагрузка на арендные сервера возрасли и вам поставлена задача стать LIR и организовать свою AS чтобы перенести все сервера игры на свою инфраструктуру. После организации вашей AS коллеги из отдела DEVOPS попросили вас сделать L3VPN между 3 офисами для служебных нужд. (Рисунок 1) Данный L3VPN проработал пару недель и коллеги из отдела DEVOPS попросили вас сделать VPLS для служебных нужд.  

## <a name="section2">Цель работы</a>  

Изучить протоколы BGP, MPLS и правила организации L3VPN и VPLS.

## <a name="section4">Ход работы</a>

### <a name="section4.1">Построение схемы</a>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/5d5b02f4-3798-4eb1-b3ad-4107155242e6" width=900></p>

На каждом из маршрутизаторов были настроены интерфейсы.

* Роутер NYC

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/dc788b9c-99a3-41d7-be63-ee8ca696761a" width=900></p>

* Роутер LND

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/eb140fdc-f871-4a7a-9acd-3a099654235e" width=900></p>

* Роутер LBN

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/2bb7537d-0bc3-4853-b0a7-c8a83faabc08" width=900></p>

* Роутер SVL

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/31d024d9-f791-4aec-9404-8b67cfb34946" width=900></p>

* Роутер HKI

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/13cc17cc-4b7a-4a43-8fa7-af560bc93cf5" width=900></p>

* Роутер SPB

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/af2a4f26-927d-45a8-91b4-b6d055673776" width=900></p>

### <a name="section4.1">Настройка BGP</a>

Настройки BGP, прописываются к ближайшим интерфейсам узла

Например:

* Роутер NYC

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/1c7af363-c9ff-4f76-9292-83b3ad87a4fa" width=900></p>

* Роутер LND

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/0677ff19-16d7-48e6-a156-6543f8100e39" width=900></p>

* Роутер HKI

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/416f8f8e-f7c3-4b9d-918f-d22f413facbb" width=900></p>

### <a name="section4.1">Настройка OSPF и MPLS</a>

Для настройки OSPF на всех узлах был создан bridge Lo

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/dc07d41c-f042-40a9-a4f8-315b6fda9c1e" width=900></p>

В параметрах, при заранее определенных интефейсах и создании network backbone, автоматически создаются интерфейсы OSPF

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/61125540-1183-4979-8121-f7764ed54cdd" width=900></p>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/01cfdec3-7166-4779-ae18-581e810cd89b" width=900></p>

Также было проделано на остальных роутерах

Далее настраиваем MPLS сеть на примере лондонского роутера

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/3988a5f5-ace0-44f1-a1c4-96f5c5cdde6b" width=900></p>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/4a8f162f-dfe0-4b59-ac92-7441d0757b22" width=900></p>


### <a name="section4.1">Настройка VRF</a>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/bd78cdd0-8d32-43b3-9dd4-adacd2beaa3a" width=900></p>

Для того чтобы собрать VRF (технология, позволяющая реализовывать на базе одного физического маршрутизатора иметь несколько виртуальных – каждого со своей независимой таблицей маршрутизации) на 3 роутерах и их ip адреса не были доступны в таблице маршрутизации main на каждом роутере, связанном с PC создаем интерфесы на вкладке ip-routes-vrf

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/78155424-5429-4563-884f-68eabfe60508)

Далее, при условии, что в настроены iBGP с route reflector кластером на узле LND и включены нужные технологии на всех роутерах в настройках BGP, в появившейся вкладке VPN4 автоматически появятся маршруты

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/d8d64308-78b1-4369-880e-a45237968037" width=900></p>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/172176c8-23df-49cb-b754-9a3c2a5abacb" width=900></p>

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/0006a94d-a583-4471-a7b9-1cdeaa6248a2" width=900></p>

### <a name="section4.1">Таблицы маршрутизации роутера NYC</a>

* Таблица маршрутизации, после настроек всех роутеров (main)

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9fc4737a-339d-4d0a-98c7-1aea75b5b96d" width=900></p>

* Таблица маршрутизации, после настроек всех роутеров (VRF_DEVOPS)

1. NYC

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/63e62737-05dd-4efb-93b8-97c48df591a0" width=900></p>

2. SPB

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/4ca53163-abc3-4216-9a9a-55c011669b9f" width=900></p>

3. SVL

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/bf0f0226-6283-4f7c-9516-1ef0f742118e" width=900></p>


### <a name="section4.1">Проверка связи VRF</a>

* PC2 -> PC1 и PC2 -> PC3

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/ef986df7-6ad8-4b75-a0d1-7f7fc7d02576" width=900></p>

* PC1 -> PC3 и PC1 -> PC2

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/b9cc596e-29e7-4dd6-8ca0-1eaa44cbd31b" width=900></p>

* PC3 -> PC2 и PC3 -> PC1

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/e06d0c7b-81e4-4296-bd5e-ba92a3a7020e" width=900></p>

### <a name="section4.1">Настройка VPLS</a>

После мы разобрали VRF на 3 роутерах, на узлах был настроен VPLS в этой конфигурации указываются параметры, такие как MAC-адрес, максимальный размер передаваемого кадра и адрес конечной точки удаленного узла, необходимые для обеспечения виртуальной приватной службы LAN.  

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9da88d11-baa5-42b6-b5b6-acf08148eabe" width=900></p>

Видно, в какой момент были отправлены icmp запросы.

## <a name="section4.5">Вывод</a>

В данной лабораторной работе, мы на праактике изучили протоколы BGP, MPLS и правила организации L3VPN и VPLS.






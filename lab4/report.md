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

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/5d5b02f4-3798-4eb1-b3ad-4107155242e6" width=800></p>

На каждом из маршрутизаторов были настроены интерфейсы. На примере роутера Нью-Йорка

* Роутер NYC

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/dc788b9c-99a3-41d7-be63-ee8ca696761a" width=800></p>


### <a name="section4.1">Настройка BGP</a>

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/3f56a08b-9a67-4fa8-890b-592f4f54e37e)

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9c8f8e00-1de9-449d-b100-228f4f71ed9b)

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9023a8aa-0752-4abb-a7ee-cd25f5cdf803)

### <a name="section4.1">Настройка OSPF и MPLS</a>

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/4087cfb5-2c8f-406d-b2a3-13bbf2994979)

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/7de1eabd-b99d-4f14-b354-85f6f9c39fde)


### <a name="section4.1">Настройка VRF</a>


### <a name="section4.1">Таблицы маршрутизации роутера NYC</a>

* Таблица маршрутизации, после настроек всех роутеров (main)

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9fc4737a-339d-4d0a-98c7-1aea75b5b96d" width=800></p>

* Таблица маршрутизации, после настроек всех роутеров (VRF_DEVOPS)

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/63e62737-05dd-4efb-93b8-97c48df591a0" width=800></p>

### <a name="section4.1">Проверка связи</a>

* PC2 -> PC1 и PC2 -> PC3

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/ef986df7-6ad8-4b75-a0d1-7f7fc7d02576" width=800></p>

* PC1 -> PC3 и PC1 -> PC2

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/b9cc596e-29e7-4dd6-8ca0-1eaa44cbd31b" width=800></p>

* PC3 -> PC2 и PC3 -> PC1

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/e06d0c7b-81e4-4296-bd5e-ba92a3a7020e" width=800></p>

## <a name="section4.5">Вывод</a>






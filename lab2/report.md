University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Fomintsev Denis Ruslanovich  
Lab: Lab2  
Date of create: 10.11.2023  
Date of finished: 22.11.2023  

## Лабораторная работа №2 "Эмуляция распределенной корпоративной сети связи, настройка статической маршрутизации между филиалами"

### Оглавление
- [Описание](#section1)
- [Цель работы](#section2)
- [Ход работы](#section4)
  - [Схема сети](#section4.1)
  - [Настройка роутеров](#section4.2)
  - [Настройка компьютеров](#section4.3)
  - [Проверка доступности](#section4.4)
- [Вывод](#section4.5)
 
## <a name="section1">Описание</a>

В данной лабораторной работе вы первый раз познакомитесь с компанией "RogaIKopita Games" LLC которая занимается разработкой мобильных игр с офисами в Москве, Франкфурте и Берлине. Для обеспечения работы своих офисов "RogaIKopita Games" вам как сетевому инженеру необходимо установить 3 роутера, назначить на них IP адресацию и поднять статическую маршрутизацию. В результате работы сотрудник из Москвы должен иметь возможность обмениваться данными с сотрудником из Франкфурта или Берлина и наоборот.  

Ознакомиться с принципами планирования IP адресов, настройке статической маршрутизации и сетевыми функциями устройств.

## <a name="section4">Ход работы</a>

### <a name="section4.1">Схема сети</a>

1. Создание схемы сети описано в yaml файле, приложенной к данному отчету.
Вывод команды ```sudo containerlab graph```  
<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/f3c8e69f-edd8-4494-8c19-da2c34e4a246" width=800></p>


### <a name="section4.2">Настройка роутеров</a>

Настроим IP адреса на всех интерфейсах роутеров, создадим DHCP сервера на них в сторону клиентских устройств  
* Настройка профиля безопасности беспроводного интерфейса  
* Создание пула адресов (/ip pool)  
* Настройка DHCP-клиента (/ip dhcp-client)  
* Настройка статических маршрутов (/ip route)  
* Добавляете DHCP-сервера для интерфейса ether2 (/ip dhcp-server)   

1. Роутер MSK.

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/da3df30e-7fcc-4a35-9cba-2a73fc135885" width=800></p>
<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/773100ed-4c4d-46ab-b5cd-f611834d3617" width=800></p>

2. Роутер FRT.

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/0740e1e9-e489-4d2d-91b1-e6e06e31a9f7" width=800></p>
<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/f9918176-8190-41bc-a9f2-e01a3608f904" width=800></p>

3. Роутер BRL.

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/c22a7837-cf3c-4679-9b8f-ffb752ceeabb" width=800></p>

### <a name="section4.3">Настройка компьютеров</a>  
* Настройка IP-адреса на интерфейсе ether1  
* Настройка DHCP-клиента на интерфейсах ether1 и ether2, чтобы получить IP-конфигурацию от DHCP-сервера.
* Настройка статических маршрутов  

1. Настройка московского компьютера  

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/ea9ef124-2132-488e-ae54-cb9b8cca997f" width=800></p>

2. Настройка франкфуртского компьютера  

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/1d5ba523-590d-4e47-9510-107dc4710c5f" width=800></p>

3. Настройка берлинского компьютера  

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/27931c38-7ed6-45f2-9c11-a967f3cec9bd" width=800></p>

## <a name="section4.4">Проверка доступности</a>  

1. MSK -> BRL; MSK -> FRT

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/e35f14b9-1be4-416a-b920-a23a4a95facf" width=800></p>

2. FRT -> BRL; FRT -> MSK

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/74c85ade-67bc-4a92-b62a-8ff7d03c1f90" width=800></p>

3. BRL -> MSK; BRL -> FRT

<p align=center><img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/1244aed4-a9c5-4f2e-9fce-af3481649b0d" width=800></p>

## <a name="section4.5">Вывод</a>
В данной лабораторной работе я практически изучил планирование IP адресов, настройку статической маршрутизации и сетевые функции устройств.







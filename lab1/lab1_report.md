University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Fomintsev Denis Ruslanovich  
Lab: Lab1  
Date of create: 04.09.2023  
Date of finished: 15.09.2023  


## Лабораторная работ №1 "Установка ContainerLab и развертывание тестовой сети связи"

### Оглавление
- [Описание](#section1)
- [Цель работы](#section2)
- [Правила по оформлению](#section3)
- [Ход работы](#section4)
  - [Подготовка](#section4.1)
  - [Сеть](#section4.2)
    - [Настройка роутера R01](#section4.3)
    - [Настройка SW01.L3.01](#section4.4)
    - [Настройка SW02.L3.01](#section4.5)
    - [Настройка SW02.L3.02](#section4.6)


## <a name="section1">Описание</a>
В данной лабораторной работе вы познакомитесь с инструментом ContainerLab, развернете тестовую сеть связи, настроите оборудование на базе Linux и RouterOS.  

## <a name="section2">Цель работы</a>
Ознакомиться с инструментом ContainerLab и методами работы с ним, изучить работу VLAN, IP адресации и т.д.

## <a name="section3">Правила по оформлению</a>
Правила по оформлению отчета по лабораторной работе вы можете изучить по <a href="https://itmo-ict-faculty.github.io/introduction-in-routing/education/labs2023_2024/reportdesign/">ссылке</a>  

## <a name="section4">Ход работы</a>    

### <a name="section4.1">Подготовка</a>  
Перед началом выполнения лабораторной работы были выполнены следующие действия:  
* Установка make и клонирование репозитория <a href="https://github.com/hellt/vrnetlab">hellt/vrnetlab</a>  
* В проекте hellt/vrnetlab в папке routeros, был загружен файл chr-6.47.9.vmdk и с помощью make docker-image собран образ.  
* Установка ContainerLab, используя специальный скрипт из официального репозитория  
  ```bash -c "$(curl -sL https://get.containerlab.dev)"```

<img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9f650856-5863-47c4-9139-a0dbdab66ada" width=900>  

### <a name="section4.2">Сеть</a>
Далее создаем трехуровневую сеть связи классического предприятия.
```
name: lab1

topology:
  nodes:
    R01:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 192.168.50.2

    Linux1:
      kind: linux
      image: alpine:latest
      cmd: sleep infinity
      mgmt-ipv4: 192.168.50.3

    Linux2:
      kind: linux
      image: alpine:latest
      cmd: sleep infinity
      mgmt-ipv4: 192.168.50.4
      
    SW01.L3.01:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 192.168.50.5

    SW02.L3.01:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 192.168.50.6

    SW02.L3.02:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 192.168.50.7

  links:
      - endpoints: ["R01:eth1", "SW01.L3.01:eth1"]
      - endpoints: ["SW01.L3.01:eth2", "SW02.L3.01:eth1"]
      - endpoints: ["SW02.L3.01:eth2", "Linux1:eth1"]
      - endpoints: ["SW01.L3.01:eth3", "SW02.L3.02:eth1"]
      - endpoints: ["SW02.L3.02:eth2", "Linux2:eth1"]
      
mgmt:
  network: static
  ipv4-subnet: 192.168.50.0/24
```

* mgmt сеть - это сеть, которая используется для управления и доступа к устройству. Обычно она изолирована от других сетей, которые могут существовать на устройстве.
* CHR (Cloud Hosted Router) от MikroTik, это виртуальный маршрутизатор, который развертывается в облаке или в виртуальной среде. Для безопасного управления CHR и настройки его параметров часто используется mgmt сеть. Это позволяет администраторам удаленно подключаться к CHR и вносить изменения в его конфигурацию.

Получим следующую схему после сборки ```sudo containerlab deploy networklab.yaml```:  
```sudo containerlab graph```  

<img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/f0c03f87-e5dd-44c6-8231-44dc65dbf9d7" width=900>

### <a name="section4.3">Настройка роутера R01</a>  

<img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/84085da8-821c-4350-8eb0-93d0e3606bc9" width=900>  

Здесь:  
* Cоздаются два виртуальных интерфейса VLAN на физическом интерфейсе ether2. Один с идентификатором VLAN 10, а другой с идентификатором VLAN 20.  
* Встроенный профиль безопасности для беспроводных сетей изменяется, устанавливая параметр supplicant-identity. Это связано с идентификацией устройства в сети Wi-Fi.  
* Создаются два пула адресов DHCP: pool10 и pool20, которые предназначены для выдачи IP-адресов в сетях VLAN 10 и VLAN 20 соответственно
* Создаются два DHCP-сервера: server1 и server2, каждый из которых связан с соответствующим интерфейсом VLAN (vlan10 и vlan20). Эти серверы будут выдавать IP-адреса из соответствующих пулов адресов в их VLAN.
* Интерфейс ether1 получает адрес 195.58.228.138/30, а интерфейсы vlan10 и vlan20 получают адреса 172.20.10.1/24 и 172.20.20.1/24 соответственно.
* Добавляются настройки сетей для DHCP-серверов. Эти настройки включают адреса сетей и их шлюзы.

### <a name="section4.4">Настройка SW01.L3.01</a>  

<img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/b36b661c-e154-4725-be67-3dbe9da3bce1" width=900>  

* Создается мост с именем "bridge", который будет использоваться для объединения разных VLAN-ов.
* Добавление интерфейсов "vlanN" в мост "bridgeN", связывая их с этим мостом.
* Включение DHCP-клиента на интерфейсе "ether1". Это позволит устройству получить конфигурацию IP-адреса автоматически от DHCP-сервера.

### <a name="section4.5">Настройка SW02.L3.01</a> 

<img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/18d206bd-9110-4247-b453-cd3d56eef790" width=900>

### <a name="section4.6">Настройка SW02.L3.02</a> 

<img src="https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/c2a25201-e239-4110-8dd5-160a355d6be8" width=900>


## <a name="section5">Проверка доступности</a>

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/9e765051-2552-4c9e-a317-15aa343f025b)

![image](https://github.com/DeFomin/2023_2024-introduction_in_routing-k33212-fomintsev-d-r/assets/90705279/270bdd1c-8769-478b-8733-2d14155757a4)












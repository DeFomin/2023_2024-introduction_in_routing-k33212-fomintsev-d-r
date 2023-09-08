# 2023_2024-introduction_in_routing-k33212-fomintsev-d-r

**Все отчеты по лабораторным работам по курсу  "Введение в маршрутизацию на предприятии"**

```ContainerLab``` - это инструмент, предназначенный для управления и развертывания виртуальных сетевых лабораторий с использованием контейнеров Docker. Он позволяет создавать изолированные среды с сетевым оборудованием, таким как маршрутизаторы, коммутаторы, и серверы, внутри контейнеров
- **Определение топологий.**
- **Мультиплатформенность.** ContainerLab поддерживает различные сетевые операционные системы, такие как Cisco IOS, Juniper Junos, MikroTik RouterOS, и многие другие.
- **Лаборатории сети.** ContainerLab позволяет создавать виртуальные сетевые лаборатории, которые могут имитировать реальные сетевые среды. 

**Запуск** ```sudo containerlab deploy -t networklab.clab.yaml```  
**Остановка** ```sudo containerlab deploy --topo networklab.clab.yaml```

__Для просмотра информации о том, какие устройства и IP-адреса используют сеть__  
```arp -a```  
```nmap -sP 172.20.20.0/24```

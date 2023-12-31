# `Домашнее задание к занятию "5.1. Основы виртуализации" - Зозуля Максим`

## Задача 1

Опишите кратко, как вы поняли: в чем основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.

### Ответ

- Полная (аппаратная) виртуализация как следует из названия полностью эмулирует физический компьютер с соответствующими физическими устройствами обеспечивая тотальную изоляцию гостевой ОС*

- При паравиртуализации используются гостевые операционные системы оптимизированные для работы с гипервизором, что позволяет увеличить эффективность утилизации аппаратных ресурсов. В отличие от полной виртуализации в данной технологии допускается прямое использование гостевой ОС аппаратных ресурсов хоста*

- Виртуализация на уровне ОС реализуется без отдельного слоя гипервизора, виртуализируется пользовательское окружение ОС.*

## Задача 2

Выберите тип один из вариантов использования организации физических серверов, в зависимости от условий использования.

Организация серверов:
- физические сервера
- паравиртуализация
- виртуализация уровня ОС

Условия использования:

- Высоконагруженная база данных, чувствительная к отказу
- Различные web-приложения
- Windows системы для использования Бухгалтерским отделом 
- Системы, выполняющие высокопроизводительные расчеты на GPU

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

### Ответ

Для каждого из указанных условий использования выбор организации физических серверов, паравиртуализации или виртуализации уровня ОС может быть обоснованным в зависимости от требований и характеристик каждого конкретного случая:

Высоконагруженная база данных, чувствительная к отказу:

- Организация: Физические сервера.
Пояснение: Для высоконагруженной базы данных, особенно если она чувствительна к отказу, физические сервера предоставляют наилучшую производительность и надежность. Это позволяет минимизировать влияние виртуализации на производительность и обеспечивает более прямой доступ к аппаратным ресурсам.
Различные web-приложения:

- Организация: Паравиртуализация или виртуализация уровня ОС.
Пояснение: Для web-приложений, которые могут быть разнообразными и могут иметь разные требования к окружению, паравиртуализация или виртуализация уровня ОС предоставляют гибкость и изоляцию. Они позволяют запускать разные приложения на одном физическом сервере, обеспечивая управление ресурсами и изоляцию между приложениями.
Windows-системы для использования бухгалтерским отделом:

- Организация: Виртуализация уровня ОС.
Пояснение: Виртуализация уровня ОС позволяет запускать различные операционные системы, включая Windows, на одном физическом сервере. Это обеспечивает изоляцию между системами, что важно для бухгалтерского отдела, и позволяет эффективно управлять ресурсами.
Системы, выполняющие высокопроизводительные расчёты на GPU:

- Организация: Физические сервера.
Пояснение: Для систем, требующих высокой производительности GPU, наилучшим выбором будет физический сервер с соответствующими GPU. Виртуализация может внести дополнительный уровень абстракции и ограничить доступ к мощности GPU, поэтому физический сервер будет наиболее подходящим вариантом для обеспечения максимальной производительности в этом случае.
Итак, выбор организации зависит от конкретных требований и характеристик каждого случая, и он может варьироваться в зависимости от того, какие приоритеты у вас в данном конкретном сценарии использования.
## Задача 3

Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
2. Требуется наиболее производительное бесплатное open source решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows инфраструктуры.
4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

### Ответ

1. VMWare ESXI или Hyper-V в данном случае обладают требуемым функционалом. Учитывая преимущественность Windows based инфраструктуры возможно Hyper-V подойдёт большей ввиду лучшей совместимости с оной.

2. Могут подойти Xen, KVM  в сочетании с QEMU. KVM - это бесплатное open source-решение, встроенное в ядро Linux, которое обеспечивает хорошую производительность и поддерживает как Linux, так и Windows гостевые системы. Он также интегрирован в множество управляющих сред, таких как Virt-Manager и oVirt.

3. Microsoft Hyper-V Server имеющий наибольшую совместимость с Windows системами или как альтернатива Xen

4. Если тестирование программного продукта требует изоляции через контейнеризацию, Docker может быть хорошим выбором. Вы можете создать Docker-контейнеры с разными версиями и дистрибутивами Linux и запускать их на одной и той же хост-системе.Достаточно высокая скорость развертывания.

## Задача 4

Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, то создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.

### Ответ

Гетерогенная среда виртуализации имеет проблемы, такие как сложность управления, совместимость, сложности с безопасностью и потеря производительности. Для минимизации рисков и проблем необходимо уделять внимание обучению, стандартизации, интеграции и автоматизации, а также мониторингу производительности. Если есть выбор, то, как правило, предпочтительнее использовать одну систему управления виртуализацией, чтобы упростить управление и снизить сложность.

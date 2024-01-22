pod-to-kubermanifests(1) -- генерации kubernetes манифестов на основе поднятого podman-compose POD'а
================================

## SYNOPSIS
<pre>
pod-to-kubermanifests \
  [--type(-t) &lt;тип-разворачивания&gt;]\
  [--namespace(-n) &lt;namespace&gt;]\
  [--dir(-d) &lt;каталог-манифестов&gt;]\
  [--file(-f) &lt;имя_файла&gt;]\
  &lt;имя_POD'а&gt;\
  &lt;имя-docker-compose-файла&gt;
</pre>

## DESCRIPTION

Скрипт обеспечивает миграцию docker-compose решений в kubernetes.

До вызова скрипта необходимо с помощью команды podman-compose поднять  стек сервисов в POD'е и проверить его работоспособность (см. [podman-compose как средство миграция docker-compose решений в kubernetes](https://www.altlinux.org/Podman-compose/kubernetes#%D0%AD%D0%BA%D1%81%D0%BF%D0%BE%D1%80%D1%82_%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D0%BD%D1%83%D1%82%D0%BE%D0%B3%D0%BE_%D1%81%D1%82%D0%B5%D0%BA%D0%B0_%D0%B2_kubernetes-%D0%BC%D0%B0%D0%BD%D0%B8%D1%84%D0%B5%D1%81%D1%82%D1%8B)).

Скрипт на основе POD'а, поднятого командой `podman-compose` стека сервисов, описанного в docker-compose YML-файле, формирует kubernetes-манифесты для запуска указанного стека сервисов в kubernetes.

Манифесты при наличии флага `-d` генерируются в файлах-манифестах `<тип-разворачивания>.yml`, `service.yml`, `volumes.yml` указанного каталога. При указании флага `-f <prefix>` все манифесты помещаются в файл `<prefix>_<тип-разворачивания>.yml`.


## OPTIONS
Флаги команды:
long format | short format | значение по умолчанию | описание
------------|--------------|-----------------------|----------
--type      | -t           | pod                   |тип разворачивания: `pod` (`p`), `replicaset` (`r`), `deployment`(`d`)
--namespace | -n           | default               | kubernetes namespace
--dir       | -d           | manifests             | каталог для генерируемых манифестов (взаимоисключаем с флагом `-f`)
--file      | -f           | имя_POD'а | префикс объединенного файла-манифеста (взаимоисключаем с флагом `-d`)
Если флаги `-d`, `-f` не указаны по умолчанию принимается флаг `-f`.

Позиционные параметры:
Имя | Описание
----|-----------
имя_POD'а | имя развернутого `POD`'а
имя-docker-compose-файла | имя docker-compose файла от которого развернут `POD`

## EXAMPLES

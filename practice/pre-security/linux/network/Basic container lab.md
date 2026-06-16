## 1. Минимальная структура `topology.yml`

```yaml
name: my-lab

topology:
  nodes:
    host1:
      kind: linux
      image: alpine:latest
    host2:
      kind: linux
      image: alpine:latest

  links:
    - endpoints: ["host1:eth1", "host2:eth1"]
```

**Ключевые поля:**
- `name` — имя лабораторной (используется в именах контейнеров)
- `topology.nodes` — список устройств
  - `kind: linux` — обычный контейнер
  - `image` — любой Docker-образ с `sh`/`bash`
- `topology.links` — соединения
  - `endpoints` — пара `[узел:интерфейс]`

> Интерфейсы внутри контейнера обычно называются `eth1`, `eth2` и т.д.  
> `eth0` зарезервирован для управления.

---

## 2. Основные команды Containerlab

### Деплой (запуск) лаборатории
```bash
containerlab deploy -t topology.yml
```

### Просмотр текущих лабораторий
```bash
containerlab inspect
```
Или с деталями по конкретной:
```bash
containerlab inspect -t topology.yml
```

### Остановка и удаление лаборатории
```bash
containerlab destroy -t topology.yml
```
Удаляет контейнеры, сети, файлы состояния.

### Визуализация топологии (опционально)
```bash
containerlab graph -t topology.yml
```
Запускает веб-интерфейс с графом.

---

## 3. Работа с узлами (вход в контейнер)

```bash
# Вход с оболочкой (sh/bash)
docker exec -it <node-name> sh
# или
docker exec -it <node-name> bash
```

Имя узла формируется как:
```
<lab-name>-<node-name>
```
Пример: `my-lab-host1`

---

## 4. Ручное назначение IP-адресов внутри контейнера

```bash
# Поднять интерфейс
ip link set eth1 up

# Назначить IP-адрес
ip addr add 10.0.0.1/24 dev eth1
```

Проверка:
```bash
ip addr show eth1
ip link show eth1
```

Также мы можем задавать статические ip адреса наших хостов непосредственно в самой конфигурации yaml. Например:
```yaml
 host1:
      kind: linux
      image: alpine:latest
      exec:
        - ip addr add 10.0.0.1/24 dev eth1
        - ip link set eth1 up
```

---

## 5. Проверка связности (ping)

```bash
ping 10.0.0.2 -c 4
```

Если не пингуется — проверить:
- интерфейс поднят (`UP`)
- правильный IP/маска
- нет фаервола внутри контейнера (в Alpine/Debian по умолчанию нет)

---

## 6. Полезные нюансы 

- `eth0` — **управляющий**, не трогаем
- После `destroy` все данные в контейнерах теряются (контейнеры эфемерны)
- Можно использовать `alpine` (маленький) или `debian:latest` (полный)
- Для постоянных изменений понадобятся `bind mounts` или `startup-config` — но это позже

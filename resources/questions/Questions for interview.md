## ☀️ Pre-Security (Лето перед Семестр 3)

### 1. Базовые сети и Containerlab

**Теоретические вопросы:**

1. Опишите модель OSI и приведите примеры протоколов для каждого уровня
2. Что такое broadcast domain и collision domain? В чем разница?
3. Как работает ARP и зачем нужен gratuitous ARP?
4. Объясните разницу между частными и публичными IPv4 адресами
5. Что такое CIDR? Объясните /24, /16, /30 на практике
6. Как работает default gateway и когда он не нужен?
7. Объясните базовые принципы VLAN и trunk (802.1Q); чем это отличается от изоляции отдельными подсетями и линками в Containerlab?
8. Чем правила **nftables/iptables** сходны и чем отличаются от классических ACL на маршрутизаторе Cisco?
9. Объясните базовую механику NAT (inside/outside), SNAT/PAT
10. Как DHCP и DNS взаимодействуют в пользовательском сценарии?
11. Что такое декларативная топология Containerlab (`*.clab.yml`) и зачем нужны `nodes` / `links`?

**Практические вопросы:**

1. Как в **Containerlab** смоделировать **две изолированные подсети** с маршрутизацией между ними (без классического L2-коммутатора)?
2. Где закреплять **802.1Q trunk** и **STP**, если в Containerlab это не цель лаборатории?
3. Какие команды использовать для диагностики, если хост в лаборатории не получает IP по DHCP (**dnsmasq/Kea**, клиент, интерфейсы)?
4. Как проверить маршрут трафика между двумя подсетями (`ip route`, `show ip route` в FRR, `traceroute`)?
5. Как в лаборатории подтвердить, что **nftables/iptables** блокирует только нужный трафик (счётчики, логи, `tcpdump`)?
6. Как поднять и удалить топологию: `containerlab deploy` / `destroy`, что проверить в `inspect`?

---

### 2. Базовый Linux и сетевые утилиты

**Теоретические вопросы:**

1. Объясните структуру Linux ФС: `/etc`, `/var`, `/usr`, `/home`, `/opt`
2. В чем разница между `chmod`, `chown`, `chgrp`?
3. Как устроены пользователи и группы в Linux?
4. Что такое процессы и сигналы (SIGTERM vs SIGKILL)?
5. Как работают `ss`, `netstat`, `ip`, `ping`, `traceroute`?
6. В чем разница между `iptables` и `nftables` на базовом уровне?
7. Как работает SSH и почему важен hardening (keys-only, no root)?
8. Что такое `systemd` и как управляются сервисы?

**Практические вопросы:**

1. Как поднять Linux VM со статическим IP и SSH доступом?
2. Как посмотреть открытые порты и определить, какой процесс их слушает?
3. Как написать базовые firewall-правила для SSH + ICMP + deny all?
4. Как проверить DNS-резолвинг разными утилитами (`dig`, `nslookup`)?
5. Как автоматизировать простой backup-скрипт и запуск по расписанию?

---

## Семестр 3 - Фундамент (Сентябрь - Декабрь)

---

### 1. Сети: TCP/IP стек и фундаментальные протоколы

**Теоретические вопросы:**

1. Объясните структуру Ethernet/IP/TCP заголовков и критичные поля
2. Как работает TCP handshake/teardown и машина состояний?
3. Что такое congestion control и flow control?
4. Объясните PMTUD и типовые проблемы с MTU/MSS
5. Как работают DNS рекурсия/итерация и DNSSEC на практике?
6. В чем ключевые различия HTTP/1.1, HTTP/2 и HTTP/3 (QUIC)?
7. Как работает TLS цепочка доверия и проверка сертификатов?
8. Когда оправдано применение RAW sockets?

**Практические задачи:**

1. Реализуйте TCP эхо-сервер с несколькими клиентами
2. Напишите минимальный HTTP сервер на C
3. Создайте сканер портов (TCP connect/SYN + UDP)
4. Реализуйте DNS резолвер с итерацией по корневым серверам
5. Напишите packet sniffer на `libpcap` с базовым разбором протоколов

---

### 2. Linux: Глубокое погружение

**Теоретические вопросы:**

1. Как работают POSIX права, ACL, setuid/setgid/sticky bit?
2. Что дают `/proc` и `/sys` при диагностике инцидентов?
3. Объясните cgroups, namespaces и их связь с контейнерами
4. В чем роль `systemd` unit/timer и как правильно писать сервисы?
5. Как работает SELinux и когда он реально помогает?
6. Что такое LVM и чем полезны snapshots?

**Практические задачи:**

1. Напишите backup-скрипт с ротацией и GPG-шифрованием
2. Создайте systemd unit для собственного демона
3. Соберите firewall policy для server hardening
4. Реализуйте script-based health monitoring (CPU/RAM/disk/network)

---

### 3. C: Основы системного программирования

**Теоретические вопросы:**

1. Объясните этапы компиляции C и роль линковки
2. Как устроены указатели, выравнивание и работа с памятью?
3. В чем разница stdio (`fopen`) и syscalls (`open/read`)?
4. Что такое UB и как его искать через sanitizers/valgrind?
5. Для чего нужны `dup/dup2`, `fcntl`, `ioctl`?

**Практические задачи:**

1. Реализуйте `cat`/`grep`/`wc` (упрощенные)
2. Напишите простой конфиг-парсер (INI/TOML)
3. Реализуйте учебный аллокатор памяти

---

### 4. Python: Скриптинг и автоматизация

**Теоретические вопросы:**

1. Объясните разницу между `list`/`tuple`/`set`/`dict`
2. Как работают `*args`, `**kwargs`, context managers?
3. Что выбрать для параллелизма: threads, processes, asyncio?
4. Как безопасно вызывать внешние команды из Python?

**Практические задачи:**

1. Напишите сканер портов на Python с concurrency
2. Реализуйте HTTP клиент с разбором статуса/заголовков/тела
3. Напишите конвертер JSON <-> CSV <-> XML

---

### 5. Виртуализация

**Теоретические вопросы:**

1. В чем разница между KVM, VMware, VirtualBox?
2. Что такое NAT/bridged/host-only сети в гипервизоре?
3. Когда нужна nested virtualization и какие риски у нее?
4. Что такое Open vSwitch и зачем он в lab-сценариях?

**Практические задачи:**

1. Поднимите multi-VM lab (Linux + Windows + уязвимая VM)
2. Настройте KVM/libvirt с bridge networking
3. Напишите Vagrantfile для воспроизводимой лаборатории

---

### 6. Git и версионирование

**Теоретические вопросы:**

1. Объясните внутренности Git (blob/tree/commit/tag)
2. Merge vs rebase: когда что применять?
3. Как использовать reflog для восстановления?
4. Что такое Conventional Commits и зачем они в security-проектах?

**Практические задачи:**

1. Разрешите намеренно созданный merge conflict
2. Настройте pre-commit hooks (lint/security checks)
3. Соберите простой CI pipeline для C/Python репозитория

---

### 7. Алгоритмы и структуры данных

**Теоретические вопросы:**

1. Объясните амортизацию на примере динамического массива
2. В чем trade-off хеш-таблиц, деревьев и графовых структур?
3. Как работают BFS/DFS/топсорт на практике?
4. Какие сортировки подходят для разных профилей данных?

**Практические задачи:**

1. Реализуйте мини-библиотеку структур данных на C
2. Решите 30+ задач Easy/Medium (LeetCode)
3. Реализуйте визуализатор сортировок или RPN-калькулятор

---

### 8. Open Source Security Contributions

**Теоретические вопросы:**

1. Как корректно репортить security issue в open source?
2. В чем разница responsible disclosure и публичного disclosure?
3. Как оценивать impact/security improvements в PR?

**Практические задачи:**

1. Подготовьте 3-5 PR в security/network репозитории
2. Оформите security-improvement issue + patch + тесты

---

### 9. Продвинутый Wireshark/tshark и BPF фильтры

**Теоретические вопросы:**

1. Capture filters vs display filters: где и зачем?
2. Какие признаки beaconing/low-and-slow трафика в pcap?
3. Как строить pcap triage pipeline через `tshark` + `jq`?

**Практические задачи:**

1. Соберите набор фильтров для 10+ типовых incident-кейсов
2. Напишите CLI-анализатор pcap (top talkers, DNS anomalies)

---

### 10. BPF основы для сетевой диагностики

**Теоретические вопросы:**

1. Чем классический BPF отличается от eBPF?
2. Что такое verifier и какие ограничения он накладывает?
3. Как использовать tracepoints/kprobes для сетевых метрик?

**Практические задачи:**

1. Напишите несколько bpftrace one-liners для TCP диагностики
2. Соберите мини exporter сетевых kernel-метрик

---

## Семестр 4 - Углубление (Февраль - Июнь)

---

### 1. Операционные системы: Внутреннее устройство

**Теоретические вопросы:**

1. fork/exec/wait: как это работает в реальном приложении?
2. Что такое IPC (pipes/FIFO/msgq/shm) и когда что выбирать?
3. Как устроена виртуальная память и page faults?
4. Что такое async-signal-safe функции и почему это важно?

**Практические задачи:**

1. Реализуйте shell с пайпами и job control
2. Напишите многопоточный сервер с thread-pool

---

### 2. Основы безопасности и криптографии

**Теоретические вопросы:**

1. AES-GCM vs CBC/CTR: где и почему?
2. RSA vs ECC/Curve25519: основные trade-offs
3. Как правильно хранить пароли (Argon2/bcrypt/scrypt)?
4. Какие типовые криптоошибки чаще всего встречаются в коде?

**Практические задачи:**

1. Реализуйте secure file encryption (AES-GCM)
2. Поднимите TLS клиент/сервер с проверкой сертификата

---

### 3. Сетевые инструменты анализа и мониторинга

**Теоретические вопросы:**

1. Что дают `tcpdump`, `tshark`, `nmap`, `iperf3`, `tc`?
2. Как отличать network symptoms от application symptoms?
3. Какие метрики критичны для network observability?

**Практические задачи:**

1. Проанализируйте pcap и найдите root cause сетевой деградации
2. Напишите скрипт network-monitoring с алертами

---

### 4. Отладка сетевых приложений

**Теоретические вопросы:**

1. Как связывать `strace/ltrace` с packet-level анализом?
2. Что означает `TIME_WAIT`/`CLOSE_WAIT` и как лечить?
3. Какие типовые причины TLS handshake failure?

**Практические задачи:**

1. Разберите кейс `connection refused` end-to-end
2. Найдите утечку сокетов/дескрипторов в сервисе

---

### 5. C++: Современный стандарт и системное программирование

**Теоретические вопросы:**

1. Объясните RAII, move semantics, smart pointers
2. Когда использовать atomics и memory ordering?
3. Как строить thread-safe компоненты в сетевом коде?

**Практические задачи:**

1. Реализуйте thread pool
2. Напишите потокобезопасный логгер

---

### 6. Проектирование сетей

**Теоретические вопросы:**

1. Как проектировать сегментацию VLAN + ACL + routing domains?
2. OSPF vs BGP: где что предпочтительнее?
3. Как строить QoS профиль под voice/video/data?

**Практические задачи:**

1. Спроектируйте и защитите сеть кампуса/офиса (diagram + policy)
2. Настройте NAT + ACL + межвлановую маршрутизацию

---

### 7. Физическая лаборатория (реальное оборудование)

**Теоретические вопросы:**

1. Как выполняется baseline hardening сетевого оборудования?
2. Что такое port security/storm control/BPDU guard?
3. Как безопасно организовать mgmt plane?

**Практические задачи:**

1. Настройте switch/router с нуля по чек-листу
2. Проверьте защиту от loop и rogue device сценариев

---

### 8. Введение в пентест

**Теоретические вопросы:**

1. Этапы pentest lifecycle и правила engagement
2. Recon vs enumeration vs exploitation vs post-exploitation
3. Что входит в качественный pentest report?

**Практические задачи:**

1. Пройдите 5-10 lab-машин с оформлением отчета
2. Проведите controlled exploitation через Metasploit

---

### 9. Rust для сетевого программирования

**Теоретические вопросы:**

1. Ownership/borrowing в сетевом async-коде
2. Tokio runtime и backpressure паттерны
3. Как избегать memory bloat в long-running сервисах?

**Практические задачи:**

1. Напишите async TCP/HTTP сервис на Rust
2. Сравните latency/throughput с реализацией на Go/C

---

### 10. Продвинутая отладка сетевых приложений

**Теоретические вопросы:**

1. Как разбирать сложные race-condition кейсы в production?
2. Как строить корреляцию logs + traces + packets?
3. Какие anti-patterns чаще ломают highload networking?

**Практические задачи:**

1. Диагностируйте деградацию p99 latency на реальном стенде
2. Подготовьте postmortem с корректирующими мерами

---

### 11. Дизайн и реверс кастомных протоколов

**Теоретические вопросы:**

1. Как проектировать message framing/state machine протокола?
2. Какие ошибки в custom crypto/design встречаются чаще всего?
3. Как строить фаззинг стратегию для бинарного протокола?

**Практические задачи:**

1. Сделайте reverse неизвестного протокола по pcap
2. Реализуйте базовый фреймворк протокол-фаззинга

---

## Семестр 5 - Специализация (Февраль - Июнь)

---

### 1. Продвинутая сетевая безопасность

**Теоретические вопросы:**

1. Разберите ключевые L2/L3 атаки: ARP spoofing, IP spoofing, DHCP abuse
2. Как работают IDS/IPS и где границы их эффективности?
3. Как выявлять lateral movement по сетевым признакам?

**Практические задачи:**

1. Настройте детект scanning/beaconing аномалий
2. Напишите набор правил для Suricata/Zeek

---

### 2. Файрволы и сетевая защита

**Теоретические вопросы:**

1. Stateful vs stateless filtering: trade-offs и риски
2. Как проектировать egress controls и deny-by-default?
3. IPSec/WireGuard/OpenVPN: где что предпочтительнее?

**Практические задачи:**

1. Реализуйте firewall policy с логированием и audit trail
2. Поднимите VPN сервер с MFA и ограниченным доступом

---

### 3. Go: Высоконагруженные сетевые сервисы

**Теоретические вопросы:**

1. Как работают goroutines/channels/select в highload контуре?
2. Что дает `context` для cancel/deadline propagation?
3. Как реализовать retries/circuit breaker/bulkhead?

**Практические задачи:**

1. Напишите API gateway с rate limiting и tracing
2. Поднимите gRPC сервис с нагрузочными тестами

---

### 4. Docker и контейнеризация

**Теоретические вопросы:**

1. Как устроены image layers и runtime security границы?
2. Что такое rootless containers и capability dropping?
3. Как защищать supply chain контейнеров?

**Практические задачи:**

1. Соберите multi-stage Dockerfile со security hardening
2. Настройте docker-compose стек с сетевой сегментацией

---

### 5. Kubernetes Networking

**Теоретические вопросы:**

1. Что такое CNI и как он влияет на security posture?
2. Как работают Services/Ingress/NetworkPolicy?
3. Какие риски несет kube-proxy и metadata exposure?

**Практические задачи:**

1. Поднимите k8s lab и включите строгие NetworkPolicy
2. Проверьте deny-by-default и observability сетевого трафика

---

### 6. Базы данных для сетевых приложений

**Теоретические вопросы:**

1. Как устроены транзакции/индексы в PostgreSQL?
2. Как предотвращать SQL injection в backend сервисах?
3. Где оправдан Redis cache/pubsub?

**Практические задачи:**

1. Реализуйте secure logging pipeline на PostgreSQL
2. Добавьте Redis cache layer с метриками hit/miss

---

### 7. Производительность сетевых приложений

**Теоретические вопросы:**

1. Что такое zero-copy (`sendfile`, `io_uring`) и его ограничения?
2. Как проектировать rate limiting для API?
3. Как анализировать p95/p99 latency и throughput bottlenecks?

**Практические задачи:**

1. Проведите бенчмарк HTTP сервиса и выявите bottlenecks
2. Подготовьте performance optimization report

---

### 8. Мониторинг сети: Prometheus + Grafana

**Теоретические вопросы:**

1. Как устроена архитектура Prometheus и scraping model?
2. Что важно в PromQL для security/network use-cases?
3. Как строить actionable alerts без alert fatigue?

**Практические задачи:**

1. Настройте exporters + dashboard + alert rules
2. Соберите панель по latency/errors/retransmits/drops

---

### 9. Python для автоматизации пентеста

**Теоретические вопросы:**

1. Как использовать Scapy для packet crafting и replay?
2. Когда лучше asyncio, а когда multiprocessing?
3. Как безопасно проектировать offensive automation tooling?

**Практические задачи:**

1. Напишите async scanner/recon tool
2. Сделайте pcap analyzer с IOC enrichment

---

### 10. Red Team Infrastructure

**Теоретические вопросы:**

1. Как строить C2 инфраструктуру с redirectors и OPSEC?
2. Что такое malleable C2 profile и зачем он нужен?
3. Какие ошибки в infra OPSEC чаще всего деанонимизируют операцию?

**Практические задачи:**

1. Соберите lab C2 инфраструктуру (teamserver + redirector)
2. Проведите базовый OPSEC review и hardening

---

### 11. Active Directory: Атаки и защита

**Теоретические вопросы:**

1. Как работают Kerberoasting/AS-REP Roasting/DCSync?
2. Что такое delegation abuse и почему он опасен?
3. Как обнаруживать AD атаки по логам и сетевой телеметрии?

**Практические задачи:**

1. Пройдите AD lab сценарий от initial access до DA
2. Подготовьте detection/use-case карту по ATT&CK

---

### 12. EDR/AV Evasion

**Теоретические вопросы:**

1. Какие источники телеметрии использует EDR (ETW, hooks, AMSI)?
2. Что такое direct syscalls/unhooking и их ограничения?
3. Как отличать red-team research от вредоносной практики?

**Практические задачи:**

1. Проведите controlled bypass testing в изолированной lab-среде
2. Подготовьте defensive рекомендации по hardening/детекту

---

### 13. OSINT и External Recon

**Теоретические вопросы:**

1. Какие OSINT источники полезны для attack surface mapping?
2. Как валидировать качество найденных данных и избегать false leads?
3. Юридические/этические границы внешней разведки

**Практические задачи:**

1. Проведите reconnaissance выбранной тестовой организации (легально)
2. Сформируйте prioritized external attack surface report

---

### 14. Custom C2 Framework Engineering

**Теоретические вопросы:**

1. Что включает архитектура C2 (agent, transport, tasking, OPSEC)?
2. Как выбирать транспорт (HTTP/DNS/QUIC/custom)?
3. Как строить безопасный протокол task/result обмена?

**Практические задачи:**

1. Реализуйте учебный C2 прототип с базовыми задачами
2. Добавьте telemetry/kill-switch/операционное логирование

---

### 15. Advanced AD Attacks: ESC1-ESC8 и делегации

**Теоретические вопросы:**

1. Что такое AD CS abuse (ESC paths) и почему это критично?
2. RBCD/Shadow Credentials/ACL abuse: как работает эскалация?
3. Какие defensive controls наиболее эффективны?

**Практические задачи:**

1. Воспроизведите 1-2 ADCS abuse кейса в lab
2. Подготовьте remediation roadmap для AD/PKI команды

---

### 16. EDR/AV Evasion Engineering

**Теоретические вопросы:**

1. Чем engineering подход отличается от ad-hoc bypass?
2. Как оценивать устойчивость bypass техники во времени?
3. Какие метрики использовать в purple validation цикле?

**Практические задачи:**

1. Сделайте controlled test-matrix bypass/defense
2. Оформите результат в формате безопасного R&D отчета

---

## Семестр 6 - Продвинутые темы (Сентябрь - Декабрь)

---

### Дорожка A: Red Team (Атакующий пентест)

#### 1. Атаки и эксплуатация сетей

**Теоретические вопросы:**

1. Как строятся MITM цепочки и где они ломаются?
2. Какие признаки успешного L2/L3/L7 pivot?
3. Как безопасно валидировать findings в red-team контуре?

**Практические задачи:**

1. Проведите controlled network attack chain в lab
2. Подготовьте полный technical report + detections

#### 2. Продвинутый пентест и Red Team

**Теоретические вопросы:**

1. Что такое realistic adversary emulation?
2. Как проектировать persistence/lateral movement с учетом OPSEC?
3. Какие KPI показывают зрелость Red Team программы?

**Практические задачи:**

1. Проведите мини-операцию с постэксплуатацией и отчётностью
2. Сопоставьте действия с ATT&CK и detection coverage

#### 3. Custom Malware Development / Rust-C Development

**Теоретические вопросы:**

1. Какие компоненты включает implant архитектура?
2. Как строится secure tasking/protocol design?
3. Какие защитные меры должны сопровождать исследование?

**Практические задачи:**

1. Реализуйте учебный agent prototype в изолированной среде
2. Подготовьте defensive detections к его поведенческому профилю

#### 4. Phishing и Watering Hole / 2FA Bypass

**Теоретические вопросы:**

1. Как устроены современные phishing kill chains?
2. В чем разница между credential phishing и token theft?
3. Какие контрмеры реально снижают риск compromise?

**Практические задачи:**

1. Проведите симуляцию phishing кампании в lab
2. Подготовьте user-awareness + technical controls план

#### 5. Physical/Wireless Red Team Operations

**Теоретические вопросы:**

1. Какие угрозы дает физический доступ к сети?
2. Как rogue AP и wireless атаки интегрируются в kill chain?
3. Как выглядит корректный физический engagement scope?

**Практические задачи:**

1. Выполните physical-to-network attack simulation в lab
2. Подготовьте рекомендации по physical/wireless hardening

#### 6. Purple Team и Документирование

**Теоретические вопросы:**

1. Как устроен purple loop: attack -> detect -> tune -> retest?
2. Какие разделы должен содержать senior-level security report?
3. Как переводить technical findings в business risk язык?

**Практические задачи:**

1. Проведите purple exercise и измерьте TTD/TTR
2. Сформируйте executive + technical отчеты

---

### Дорожка B: Blue Team (Защита и реагирование)

#### 1. Защита и обнаружение вторжений (расширенная)

**Теоретические вопросы:**

1. Как проектировать SIEM ingestion/normalization/correlation pipeline?
2. Как тюнить правила, сохраняя баланс precision/recall?
3. Что дает интеграция IDS + EDR + threat intel?

**Практические задачи:**

1. Разверните SIEM стенд с кастомными правилами
2. Реализуйте сценарии correlation + suppression + alert triage

#### 2. DFIR

**Теоретические вопросы:**

1. Почему chain of custody критичен для расследования?
2. Как собирать и анализировать volatile artifacts?
3. Как строить единую timeline host/network/cloud?

**Практические задачи:**

1. Проведите end-to-end incident investigation
2. Подготовьте forensic report с evidence references

#### 3. Threat Hunting с Sigma

**Теоретические вопросы:**

1. Как строить hypothesis-driven hunting?
2. Как конвертировать и валидировать Sigma под разные SIEM?
3. Что означает ATT&CK coverage depth?

**Практические задачи:**

1. Напишите 10+ Sigma правил и прогоните через CI
2. Проведите active hunt на наборе логов

#### 4. Advanced SIEM Engineering

**Теоретические вопросы:**

1. Как проектировать detection-as-code pipeline?
2. Как измерять качество детектов (precision/recall/MTTD)?
3. Как управлять версионированием и regression тестами правил?

**Практические задачи:**

1. Реализуйте detection CI/CD pipeline
2. Настройте автоматическую проверку правил на sample events

#### 5. DFIR Toolkit Automation

**Теоретические вопросы:**

1. Что включать в automated triage toolkit?
2. Как стандартизировать evidence packaging?
3. Какие метрики качества IR automation важны?

**Практические задачи:**

1. Напишите DFIR collector toolkit (Python/Bash)
2. Автоматизируйте генерацию incident timeline

---

### Общие разделы для обеих дорожек

### 4. Облачные сети и безопасность

**Теоретические вопросы:**

1. Как проектировать secure VPC/VNet сегментацию?
2. Security Groups vs NACL: где и как лучше применять?
3. Какие риски несет serverless (Function URLs, role abuse, chaining)?
4. Как анализировать VPC Flow Logs для detection use-cases?

**Практические задачи:**

1. Поднимите AWS/Azure сеть с private/public сегментами
2. Настройте cloud hardening baseline + posture scanning

---

### 5. Web Application Firewall

**Теоретические вопросы:**

1. Managed rules vs custom rules: как балансировать?
2. Как проектировать rate limiting для API?
3. Как интегрировать WAF логи в SIEM/SOAR?

**Практические задачи:**

1. Настройте WAF policy под OWASP Top 10
2. Реализуйте Geo/ASN/bot-aware ограничения

---

### 6. Беспроводные сети и безопасность

**Теоретические вопросы:**

1. WPA2 vs WPA3 (SAE): ключевые отличия в защите
2. Как работают Evil Twin/rogue AP атаки?
3. Какие меры лучше всего защищают enterprise Wi-Fi?

**Практические задачи:**

1. Выполните controlled Wi-Fi assessment
2. Подготовьте wireless hardening checklist

---

### 7. Анализ вредоносного ПО

**Теоретические вопросы:**

1. Статический vs динамический анализ: когда и что эффективнее?
2. Как выявлять packers/obfuscation и C2 шаблоны?
3. Как писать устойчивые YARA правила?

**Практические задачи:**

1. Проанализируйте sample malware и извлеките IOC/TTP
2. Подготовьте YARA pack и validation отчет

---

### 8. Reverse Engineering сетевых протоколов

**Теоретические вопросы:**

1. Как восстановить state machine неизвестного протокола?
2. Как распознавать custom crypto и его слабости?
3. Как строить эффективный протокол-фаззинг?

**Практические задачи:**

1. Reverse protocol из pcap + бинарника
2. Напишите фаззер и задокументируйте crash triage

---

### 9. SD-WAN и SASE

**Теоретические вопросы:**

1. Что меняет переход от WAN к SD-WAN/SASE архитектуре?
2. Какие security controls обязательны на branch edge?
3. Как реализуется Zero Trust в SD-WAN/SSE контуре?

**Практические задачи:**

1. Спроектируйте SD-WAN/SASE reference architecture
2. Подготовьте risk model и remediation plan

---

### 10. VPN (углублённо)

**Теоретические вопросы:**

1. IKEv2/IPSec: ключевые стадии и типовые проблемы
2. WireGuard: архитектурные преимущества и ограничения
3. Какие риски несет split tunneling?

**Практические задачи:**

1. Настройте IPSec + WireGuard в lab и сравните
2. Добавьте MFA, логи и контроль доступа

---

### 11. eBPF для сетевой безопасности и мониторинга

**Теоретические вопросы:**

1. Какие преимущества дает eBPF/XDP для сетевой безопасности?
2. Как устроены BPF maps и attach points?
3. Какие риски и ограничения у eBPF в production?

**Практические задачи:**

1. Реализуйте eBPF/bpftrace сценарии для network observability
2. Подготовьте XDP фильтр с метриками и тестом под нагрузкой

---

## Семестр 7 - Enterprise Security Engineering (Февраль - Июнь)

---

### 1. eBPF/XDP Security Engineering (enterprise)
### 2. Высоконагруженные сетевые сервисы на Go/Rust
### 3. Cloud-native Security Architecture
### 4. Purple Team Engineering и метрики
### 5. Leadership Track для Red Team Lead / Architect
### 6. Cilium и eBPF Security Platform
### 7. Highload Rust Networking
### 8. Cloud-native Security Operations

**Теоретические вопросы (общий enterprise-блок):**

1. Как проектировать enterprise detection/response платформу?
2. Какие архитектурные решения критичны для 100k RPS security-гейтвеев?
3. Как внедрять Zero Trust и cloud-native controls без деградации бизнеса?
4. Как измерять зрелость purple/security engineering программы?
5. Какие лидерские компетенции нужны Red Team Lead/Security Architect?

**Практические задачи (общий enterprise-блок):**

1. Реализуйте enterprise lab: eBPF telemetry + cloud controls + detections
2. Подготовьте architecture review и защиту перед mock-комиссией
3. Постройте dashboard метрик TTD/TTR/coverage и remediation pipeline

---

## Семестр 8 - Финализация (Сентябрь - Декабрь)

---

### 1. Финальный проект
### 2. Code Review чужого сетевого проекта
### 3. Глубокая специализация
### 4. Поиск работы
### 5. Разбор 20 реальных сетевых кейсов
### 6. Дополнительные темы
### 7. Advanced Code Review Mastery
### 8. Анализ реальных инцидентов
### 9. Advanced Certification Prep

**Теоретические вопросы:**

1. Как обосновать архитектурные решения финального проекта?
2. Какие критерии отличают senior-level code review от junior review?
3. Как формировать специализацию под конкретную роль (Red/Blue/Architect)?
4. Как готовиться к case-based interview в network security?
5. Как приоритизировать подготовку к OSEP/OSWE/CRTO/AWS Security?

**Практические задачи:**

1. Завершите финальный проект с документацией и тест-планом
2. Проведите 2-3 глубоких code review и предложите патчи
3. Разберите 20 кейсов troubleshooting/security interview формата
4. Подготовьте portfolio + resume + interview story pack

---

## Семестр 9 - Red Team Mastery & Architecture (Финальный уровень)

---

### 1. Enterprise Red Team Operations
### 2. Advanced C2 Engineering
### 3. Custom Implant Development
### 4. Purple Team Engineering at Scale
### 5. Security Architecture & Zero Trust
### 6. Leadership и управление Red Team программой
### 7. Interview & Career Mastery
### 8. Финальная интеграция и APT эмуляция

**Теоретические вопросы:**

1. Как планировать enterprise-level Red Team операцию end-to-end?
2. Какие требования к C2/implant engineering для realistic emulation?
3. Как встроить purple validation в continuous security program?
4. Как защищать Zero Trust архитектуру от сложных attack chains?
5. Как масштабировать Red Team программу и управлять рисками?

**Практические задачи:**

1. Проведите комплексную APT-эмуляцию в изолированной lab среде
2. Подготовьте полный пакет отчетности (exec + tech + remediation roadmap)
3. Сформируйте финальный career package под роли Lead/Architect


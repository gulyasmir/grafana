# Инструкция по развертыванию Prometheus и Grafana

Скачайте репозиторий командой `git clone https://github.com/gulyasmir/grafana.git`

### Развёртывание Prometheus

Запустить командой
`docker-compose up -d`

По адресу [`<span class="code-inline__content">http://locahost:8080/metrics</span>`](http://locahost:8080/metrics) можно получить метрики.

Если перейти на вкладку targets [`<span class="code-inline__content">http://localhost:9090/targets?search=</span>`](http://localhost:9090/targets?search=), то можно увидеть источник метрик

в Prometheus в разделе Targets [`<span class="code-inline__content">http://localhost:9090/targets?search=</span>`](http://localhost:9090/targets?search=) вы увидите новый сервис app

Метрики [`<span class="code-inline__content">http://localhost:8080/rand_metrics</span>`](http://localhost:8080/rand_metrics)


### Grafana

**.**Откройте [\`](http://localhost:3000/)[http://localhost:3000](http://localhost:3000/) admin/admin\`.

Добавьте Prometheus: Connections→ Add new connection → «Prometheus» в строке поиска.

В настройках напишите ссылку на сервер с метриками [`<span class="code-inline__content">http://prometheus:9090</span>`](http://prometheus:9090/). Сохраните (кнопка внизу)

Добавьте новый дашборд. Добавьте метрики, нажав Add visualization.

Заполните название метрики `<span class="code-inline__content">http_request_duration_count</span>` и нажмите Run queries.

Заполните название метрики `<span class="code-inline__content">http_request_duration_bucket</span>`, в функциях агрегации выберите Avg by (средняя) по метке `<span class="code-inline__content">le</span>` (время меньше, чем из наших синтетических метрик) и нажмите Run queries.  Нарисуется график, дальше исправьте Title в Panel Options и нажмите Save. По итогу у вас получится  вариант RED.

Заполните название метрики `<span class="code-inline__content">http_request_duration_count</span>` и `<span class="code-inline__content">label = 500</span>` (ошибочные запросы) и нажмите Run queries.


*Полезные ссылки:*

[Официальная документация](https://prometheus.io/docs/instrumenting/exposition_formats/)

[Google Cloud Tech **Custom Metrics with Prometheus**](https://www.youtube.com/watch?app=desktop&v=XToKHYXSUyc)

[Аня Сокол **Error Budget, SLO и мониторинг: советы для начинающих SRE-инженеров](https://habr.com/ru/companies/slurm/articles/715762/)

[Подробная настройка алертов в Grafana](https://blog.kvv213.com/2023/12/grafana-alerting-ponyat-i-prostit/)

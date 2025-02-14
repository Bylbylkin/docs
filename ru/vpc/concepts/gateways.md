# Шлюзы

## NAT-шлюз {#nat-gateway}

_NAT-шлюз_ позволяет предоставлять доступ в интернет облачным ресурсам, не назначая им публичные IP-адреса. Вместо этого они будут выходить в интернет через NAT-шлюз, который получит адрес из отдельного диапазона публичных IP-адресов. Шлюз — региональный ресурс, который присутствует во всех зонах доступности. [Управлять шлюзами](../operations/create-nat-gateway.md) можно через консоль управления, с помощью CLI, Terraform или API.

Чтобы направить трафик через шлюз, нужно указать его в [таблице маршрутизации](static-routes.md) в качестве next hop. Сейчас с NAT-шлюзом можно использовать только маршрут с префиксом назначения `0.0.0.0/0`: весь трафик за пределы сети будет направляться через шлюз.

Если сетевому интерфейсу ВМ назначен [публичный IP-адрес](address.md#public-addresses), а в подсети, к которой этот интерфейс подключен, есть таблица маршрутизации с настроенным шлюзом, то выходить в интернет ВМ будет с публичного IP-адреса, а не через шлюз. Использовать зарезервированные публичные IP-адреса для шлюзов сейчас нельзя.

{% note warning %}

Обратите внимание, что NAT-шлюз заменит функцию [NAT в интернет](../operations/enable-nat.md) для подсетей. Если вы выключите в подсети NAT в интернет, то не сможете включить его — вместо него нужно будет использовать NAT-шлюз. 

{% endnote %}



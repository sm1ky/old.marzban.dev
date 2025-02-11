---
author: nikolas
date: 2024-01-18
title: Про фрагментацию
---

![](https://s3.marzban.ru/img/blog/IMG_20240118_042422.jpg)
## TLS 

Протокол TLS обеспечивает конфиденциальность, подлинность и целостность интернет-трафика в клиент-серверной среде. Хотя TLS может шифровать произвольные данные приложений, он преимущественно используется для шифрования HTTP-соединений. Google Chrome сообщает, что около 93% его соединений осуществляются через HTTPS (HTTP+TLS). Шифрование HTTP делает соединения HTTPS устойчивыми к анализу цензоров таких полей, как заголовок Host HTTP. Однако, прежде чем TLS может передавать зашифрованные данные приложений, он выполняет так называемое "рукопожатие". Это незашифрованное рукопожатие содержит указание имени сервера (SNI), которое отражает содержимое заголовка Host HTTP. Рукопожатие изображено ниже.
![](https://upb-syssec.github.io/assets/img/2023/06/record-frag/handshake-dark.svg)
Цензоры по всему миру используют расширение SNI для облегчения цензуры HTTPS-соединений. В качестве контрмеры IETF предложила ESNI и ECH. Оба эти метода шифруют расширение SNI в сообщении ClientHello. К сожалению, стандарт все еще находится в стадии разработки, и его распространение далеко от широкого. Единственный сайт, для которого мы смогли найти действующую конфигурацию ECH, - это тестовый сервер Cloudflare. Медленное внедрение ECH требует промежуточных решений для обхода цензуры SNI. Одним из таких решений является фрагментация сообщений TLS на несколько фрагментов TCP, известная как фрагментация TCP.
## Фрагментация TCP

TCP - это протокол, основанный на потоках, через который пользователи и приложения могут отправлять данные, используя абстрактные потоки данных. Эти потоки данных преобразуются TCP в фактические сетевые пакеты, называемые сегментами TCP. Каждый сегмент TCP может содержать либо полные сообщения приложений, либо только их части. Последнее называется фрагментацией TCP.
![](https://upb-syssec.github.io/assets/img/2023/06/record-frag/tcp_frag-dark.svg)
Интересно, что фрагментацию TCP можно использовать для обхода цензуры, так как она усложняет анализ трафика. В приведенном выше примере цензор должен объединить оба фрагмента TCP, чтобы правильно идентифицировать назначение запроса GET. Это фактически заставляет цензора поддерживать состояние и выделять дорогостоящую память для анализа каждого соединения. Из-за затрат на анализ фрагментации TCP многие цензоры в прошлом игнорировали ее. Поскольку она оказалась успешной, фрагментацию TCP реализовали в различных инструментах обхода цензуры. Однако недавно китайский цензор стал более продвинутым и начал обрабатывать фрагментацию TCP.

## Фрагментация записей TLS

Хотя сообщения TLS могут быть фрагментированы на несколько сегментов TCP, они также могут быть фрагментированы на уровне TLS. Это возможно, потому что слой TLS состоит из двух разных уровней: уровня сообщений TLS и уровня записей TLS. На уровне записей TLS каждое сообщение TLS обернуто в структуру записи TLS. Самое важное, что одно сообщение TLS может быть разделено на несколько записей TLS, что приводит к фрагментации записей TLS.
![](https://upb-syssec.github.io/assets/img/2023/06/record-frag/record_frag-dark.svg)
В этом примере расширение SNI разделено на разные записи TLS. Подобно фрагментации TCP, это заставляет цензора поддерживать состояние и выделять память для потенциальной пересборки. Насколько нам известно, фрагментацию записей TLS была предложена для обхода цензуры только Томасом Порнином с 2014 года. Мы не знаем ни об одном анализе или реализации фрагментации записей TLS как техники обхода цензуры. Сегодня мы преодолеваем этот разрыв и эффективно вновь открываем фрагментацию записей TLS как жизнеспособную технику обхода цензуры.

# Nginx功能概述

## HTTP基础功能

* 处理静态文件，索引文件以及自动索引；
* 反向代理加速\(无缓存\)，简单的负载均衡和容错；
* FastCGI，简单的负载均衡和容错；
* 模块化的结构。过滤器包括gzipping, byte ranges, chunked responses, 以及 SSI-filter 。在SSI过滤器中，到同一个 proxy 或者 FastCGI 的多个子请求并发处理；
* SSL 和 TLS SNI 支持；

## IMAP/POP3 代理服务功能:

* 使用外部 HTTP 认证服务器重定向用户到 IMAP/POP3 后端；
* 使用外部 HTTP 认证服务器认证用户后连接重定向到内部的 SMTP 后端；
* 认证方法：
* POP3: POP3 USER/PASS, APOP, AUTH LOGIN PLAIN CRAM-MD5;
* IMAP: IMAP LOGIN;
* SMTP: AUTH LOGIN PLAIN CRAM-MD5;
* SSL 支持；
* 在 IMAP 和 POP3 模式下的 STARTTLS 和 STLS 支持；

## 支持的操作系统:

* FreeBSD 3.x, 4.x, 5.x, 6.x i386; FreeBSD 5.x, 6.x amd64;
* Linux 2.2, 2.4, 2.6 i386; Linux 2.6 amd64;
* Solaris 8 i386; Solaris 9 i386 and sun4u; Solaris 10 i386;
* MacOS X \(10.4\) PPC;

## 结构与扩展:

* 一个主进程和多个工作进程。工作进程是单线程的，且不需要特殊授权即可运行；
* kqueue \(FreeBSD 4.1+\), epoll \(Linux 2.6+\), rt signals \(Linux 2.2.19+\), /dev/poll \(Solaris 7 11/99+\), select, 以及 poll 支持；
* kqueue支持的不同功能包括 EV\_CLEAR, EV\_DISABLE （临时禁止事件）， NOTE\_LOWAT, EV\_EOF, 有效数据的数目，错误代码；
* sendfile \(FreeBSD 3.1+\), sendfile \(Linux 2.2+\), sendfile64 \(Linux 2.4.21+\), 和 sendfilev \(Solaris 8 7/01+\) 支持；
* 输入过滤 \(FreeBSD 4.1+\) 以及 TCP\_DEFER\_ACCEPT \(Linux 2.4+\) 支持；
* 10,000 非活动的 HTTP keep-alive 连接仅需要 2.5M 内存。
* 最小化的数据拷贝操作；

## 其他HTTP功能:

* 基于IP 和名称的虚拟主机服务；
* Memcached 的 GET 接口；
* 支持 keep-alive 和管道连接；
* 灵活简单的配置；
* 重新配置和在线升级而无须中断客户的工作进程；
* 可定制的访问日志，日志写入缓存，以及快捷的日志回卷；
* 4xx-5xx 错误代码重定向；
* 基于 PCRE 的 rewrite 重写模块；
* 基于客户端 IP 地址和 HTTP 基本认证的访问控制；
* PUT, DELETE, 和 MKCOL 方法；
* 支持 FLV （Flash 视频）；
* 带宽限制；

## 实验特性:

* 内嵌的`perl`
* 通过`aio_read() / aio_write()`的套接字工作的实验模块，仅在 FreeBSD 下。
* 对线程的实验化支持，FreeBSD 4.x 的实现基于 rfork\(\)




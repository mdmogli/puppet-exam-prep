# Agent-server HTTPS communications

[INDEX](../../README.md)

## Overview:
Agents and primary server communicate via mutually authenticated HTTPS using client certificates. Puppet reuses connections by sending ***Connection: Keep-Alive*** in HTTP requests. This reduces transport layer security (TLS) overhead, improving performance for runs with dozens of HTTPS requests.

You can configure the Keep-Alive duration using the **http_keepalive_timeout** setting.
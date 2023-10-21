## 1.3.3 - 2023-10-21

- 📝 Fix websocket problem where options would disappear as soon as you typed them in the web UI
- 📝 Tidy up some log output
- 📝 Update developer docs

## 1.3.2 - 2023-10-19

- 📝 Attempt to fix 'manifest unknown' problem with build.
- 📝 Fix some github build warnings

## 1.3.1 - 2023-10-18

- 📝 Fixed issue #29 where mitmproxy would display 403 error about DNS Rebinding

## 1.3.0 - 2023-10-15

- 📝 Reinstated mitmproxy following deprecation by Poeschl
- 🔼 Updated container base images to `3.18`
- 🔼 Updated haproxy to `2.7.6.r10`
- 🔼 Updated mitmproxy to `10.1.1-r0`
- 📝 Added patching of mitmweb to allow ingress
- 📝 Port 8081 is no longer exposed for UI access - removed from config UI
- 📝 Updated readme, documentation etc to reflect new/old maintainers.

## 1.2.0 - 2022-04-05

- 🔼 Updated python3 to `3.8.10-r0`
- 🔼 Updated python3-dev to `3.8.10-r0`
- 🔼 Update openssl to `1.1.1n-r0`
- 🔼 Update openssl-dev to `1.1.1n-r0`
- 🔼 Update haproxy to `2.2.22-r0`
- 🔼 Update ca-certificates to `20211220-r0`
- 📝 Updated config.json and Readme

## 1.1.0 - 2021-04-02

- 🔨 Use ghcr.io/home-assistant for base images
- 🔼 Update openssl to `1.1.1k-r0`
- 🔼 Update openssl-dev to `1.1.1k-r0`
- 🔼 Update haproxy to `2.1.12-r0`

## 1.0.5 - 2021-03-17

- 🐛 Specifiy own S6 entrypoint, don't rely on the base image.
- 🔼 Updated python3 to `3.8.8-r0`

## 1.0.4 - 2021-03-04

- 🔼 Update python3 to `3.8.5-r1`
- 🔼 Update python3-dev to `3.8.5-r1`
- 🔼 Update haproxy to `2.1.11-r0`
- 🔼 Update openssl to `1.1.1j-r0`
- 🔼 Update openssl-dev to `1.1.1j-r0`

## 1.0.3 - 2020-11-24

- 🔼 Update haproxy to `2.1.10-r0`

## 1.0.2 - 2020-10-22

- 🔨 Start as `application` startup type

## 1.0.1 - 2020-10-06

- 🔼 Update python3 to `3.8.5-r0`
- 🔼 Update python3-dev to `3.8.5-r0`
- 🔼 Update py3-brotli to `1.0.9-r1`
- 🔼 Update ca-certificates to `20191127-r4`
- 🔼 Update haproxy to `2.1.9-r0`

## 1.0.0 - 2020-07-05

- ➕ Add mitmproxy version `5.1.1`
- ➕ Add haproxy version `2.1.4-r0`

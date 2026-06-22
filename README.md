# deb.myguard.nl

Issue tracker for the myguard packages on [deb.myguard.nl](https://deb.myguard.nl).

## Quick start

Full guide: **[deb.myguard.nl/how-to-use](https://deb.myguard.nl/how-to-use/)**

```bash
apt-get update
apt-get -y install lsb-release ca-certificates curl

# Signing key
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://deb.myguard.nl/deb.myguard.nl.gpg \
  | sudo tee /etc/apt/keyrings/deb.myguard.nl.gpg >/dev/null

# Repository (full tree for your release)
CODENAME=$(lsb_release -cs)
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/deb.myguard.nl.gpg] https://deb.myguard.nl/apt/dists/$CODENAME $CODENAME main" \
  | sudo tee /etc/apt/sources.list.d/deb.myguard.nl.list

sudo apt-get update
sudo apt-get install nginx   # or: angie
```

Want only one package? Point at its own tree instead (browse every available tree at [deb.myguard.nl/apt](https://deb.myguard.nl/apt)):

```bash
# NGINX only
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/deb.myguard.nl.gpg] https://deb.myguard.nl/apt/nginx/$CODENAME $CODENAME main" \
  | sudo tee /etc/apt/sources.list.d/deb.myguard.nl-nginx.list

# Angie only
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/deb.myguard.nl.gpg] https://deb.myguard.nl/apt/angie/$CODENAME $CODENAME main" \
  | sudo tee /etc/apt/sources.list.d/deb.myguard.nl-angie.list
```

## Links

- [`myguard.deb`](myguard.deb) — bootstrap package that configures the APT source, GPG key and pinning automatically. Install with `curl -fsSLO https://deb.myguard.nl/myguard.deb && sudo dpkg -i myguard.deb`.
- Full setup guide & repository layout: [deb.myguard.nl/how-to-use](https://deb.myguard.nl/how-to-use/)
- Browse all repository trees (full per-distro and per-package): [deb.myguard.nl/apt](https://deb.myguard.nl/apt)
- Why the repo is laid out this way (the full story): [The New deb.myguard.nl Repository Layout: Per-Package APT Trees Explained](https://deb.myguard.nl/2026/05/deb-myguard-apt-repository-layout-per-package-trees/)
- [NGINX Modules](https://deb.myguard.nl/nginx-modules/)
- [Post-Quantum Cryptography with NGINX and Angie — ML-KEM Hybrid TLS and How to Configure It](https://deb.myguard.nl/2026/05/post-quantum-cryptography-with-nginx-and-angie-ml-kem-hybrid-tls-and-how-to-configure-it/)
- [OpenSSL-NGINX — A Dedicated OpenSSL Build for NGINX and Angie](https://deb.myguard.nl/2026/05/openssl-nginx-a-dedicated-openssl-build-for-nginx-and-angie/)
- More articles: [deb.myguard.nl/articles/](https://deb.myguard.nl/articles/)

---

Created because my own forum got spammed.

Currently refactoring the package and docker building, the repos, sanitizing code and adding more testing. Let me know if something is off.

**Experimental:**
- auto update this page
- arm64 packages!
- discord! [discord.gg/UQNsFg2y](https://discord.gg/UQNsFg2y)

---

## NGINX / Angie Changelog

> Only manual interventions are logged by default — automatic builds are not.

### 2026

- **2026-06-22** Our own module: **autocert** — in-server ACME (Let's Encrypt) automatic TLS for NGINX/Angie. Obtains, serves and renews ECDSA certificates from worker 0 with no external client and no cron. Supports HTTP-01, TLS-ALPN-01 and DNS-01 (wildcards), External Account Binding (EAB), a certbot-compatible on-disk store, and multiple CAs per vhost. Ships as `libnginx-mod-http-autocert` (pulled into `nginx-full` / `angie-full`) on next build — **currently in testing**. [Article](https://deb.myguard.nl/2026/06/nginx-autocert-module/) · [GitHub](https://github.com/eilandert/nginx-autocert-module)
- **2026-06-17** Released: NGINX-1.31.2 (mainline)
- **2026-06-16** Released: ANGIE 1.11.7
- **2026-06-14** Our own module: **cache-turbo** — high-performance proxy cache acceleration for NGINX. [GitHub](https://github.com/eilandert/nginx-cache-turbo-module)
- **2026-06-14** New module on next build: `libnginx-mod-http-coraza` — OWASP Coraza WAF embedded in NGINX (libmodsecurity-compatible, CRS-ready). Built for Ubuntu Resolute and Debian Trixie.
- **2026-06-09** Our own module: **error-abuse** — auto-bans clients that rack up error responses (404/403/5xx) past a threshold, with optional cluster-wide blocking via Redis. [Article](https://deb.myguard.nl/2026/06/auto-ban-abusive-clients-in-nginx-with-the-error-abuse-module/) · [GitHub](https://github.com/eilandert/nginx-error-abuse-module)
- **2026-06-07** New module on next build (needs openssl-nginx rebuild first):
  - `libnginx-mod-ssl-fingerprint` — JA3/JA4 TLS client fingerprinting for HTTP and stream. Exposes `$ssl_fingerprint_ja3`, `$ssl_fingerprint_ja3_hash`, `$ssl_fingerprint_ja4`, `$ssl_fingerprint_ja4_o`, `$ssl_greased`; enable with `ssl_fingerprint on;`
- **2026-06-07** New patch on next build:
  - `ssl-cert-compression.patch` — TLS certificate compression (RFC 8879) with algorithm selection. Adds the directive `ssl_certificate_compression_algorithms brotli zlib zstd;` (http/stream/mail) to restrict/reorder which algorithms are offered; pairs with the upstream on/off `ssl_certificate_compression on;`.
- **2026-05-27** New builds, relaxed systemd hardening.
- **2026-05-26** New modules on next build:
  - http-auth-totp
  - http-cgi
  - http-combined-upstreams
  - http-enhanced-memc
  - http-keyval
  - http-sts
- **2026-05-25** Released: Angie 1.11.6
- **2026-05-22** Released: NGINX 1.31.1 (mainline)
- **2026-05-21** New modules on next build, whenever that might be
  - `libnginx-mod-http-access-control` — fine-grained access control rules beyond allow/deny
  - `libnginx-mod-http-array-var` — array-typed variables for use with rewrite/lua
  - `libnginx-mod-http-auth-hmac` — HMAC-signed URL authentication
  - `libnginx-mod-http-auth-internal` — internal authentication helper for protected locations
  - `libnginx-mod-http-auth-jwt` — JWT validation and claims-based authorisation
  - `libnginx-mod-http-bot-verifier` — verifies declared bots (Googlebot etc.) by reverse-DNS
  - `libnginx-mod-http-dynamic-upstream` — runtime upstream management via HTTP API
  - `libnginx-mod-http-extra-variables` — additional built-in variables for logging and routing
  - `libnginx-mod-http-footer-filter` — append content to response bodies
  - `libnginx-mod-http-form-input` — read `application/x-www-form-urlencoded` POST data into variables
  - `libnginx-mod-http-iconv` — on-the-fly character encoding conversion of responses
  - `libnginx-mod-http-internal-redirect` — issue internal redirects from config
  - `libnginx-mod-http-let` — assign expressions to variables with arithmetic and string ops
  - `libnginx-mod-http-log-var-set` — set variables specifically for use in access logs
  - `libnginx-mod-http-lua-upstream` — Lua scripting hooks into the upstream subsystem
  - `libnginx-mod-http-postgres` — direct PostgreSQL upstream backend
  - `libnginx-mod-http-proxy-var-set` — set variables on proxied requests
  - `libnginx-mod-http-rewrite-status-filter` — rewrite upstream response status codes
  - `libnginx-mod-http-server-redirect` — server-block-level redirect helper
  - `libnginx-mod-http-slowfs-cache` — slow filesystem caching layer for static assets
  - `libnginx-mod-http-sorted-querystring` — normalize querystring order for cache-key stability
  - `libnginx-mod-http-statsd` — emit nginx metrics to a StatsD collector
  - `libnginx-mod-http-ts` — MPEG-TS streaming module
  - `libnginx-mod-http-unbrotli` — transparently decompress Brotli-encoded upstream responses
  - `libnginx-mod-http-unzstd` — transparently decompress zstd-encoded upstream responses
  - `libnginx-mod-http-upload` — resumable file upload handler
  - `libnginx-mod-http-upstream-cache-vars` — expose upstream cache state as variables
  - `libnginx-mod-http-vod` — video-on-demand packaging (HLS, DASH, MSS) on the fly
  - `libnginx-mod-http-zip` — stream ZIP archives assembled from upstream files
  - `libnginx-mod-stream-sts` — stream-context traffic status monitoring
- **2026-05-20** Rebuild of NGINX/Angie, added QuickJS and latest stable version of zstd compression
- **2026-05-15** Rebuild of Angie and NGINX, added a patch to silence ktls warnings, fixed zstd compression
- **2026-05-15** Released: Angie 1.11.5
- **2026-05-13** Released: NGINX 1.31.0 (mainline) — new modules + build fixes
  - New modules added (NGINX + Angie-nextgen):
    - `libnginx-mod-http-cache-dechunk-filter` — strips chunked transfer encoding before caching responses
    - `libnginx-mod-http-compression-normalize` — normalizes `Accept-Encoding` to prevent cache fragmentation
    - `libnginx-mod-http-compression-vary` — injects correct `Vary` headers for compressed responses
    - `libnginx-mod-http-cookies-filter` — filter, strip or rewrite cookies on request & response
    - `libnginx-mod-http-cors` — Cross-Origin Resource Sharing headers (with dynamic module support patch)
    - `libnginx-mod-http-error-log-write` — write custom messages to the nginx error log from config
    - `libnginx-mod-http-limit-traffic-rate` — per-connection bandwidth / traffic rate limiting
    - `libnginx-mod-http-loop-detect` — detects and breaks proxy loops
    - `libnginx-mod-http-upstream-log` — extended upstream timing and status logging
    - `libnginx-mod-http-var` — expose nginx variables as a dynamic module
    - Update to Openssl 4.0.0 -> https://deb.myguard.nl/2026/05/openssl-4-nginx-upgrade-openssl-nginx-3-to-4/
    - Can't build on Launchpad for now, no sources for Ubuntu Resolute.
- **2026-05-11** Removed `libnginx-mod-http-proxy-connect` — Causing weird issues again, tossing it out again. Sorry.
- **2026-05-09** Updated `openssl-nginx` — fix for shared library renaming (.so path)
- **2026-05-09** Updated NGINX and Angie — rebuilt with updated openssl-nginx
- **2026-05-08** Updated `zstd-nginx-module` — comprehensive audit found and fixed severe issues. See [We audited the zstd-nginx-module and found a lot of bugs](https://deb.myguard.nl/2026/05/we-audited-the-zstd-nginx-module-and-found-a-lot-of-bugs/)
- **2026-05-08** New package: `openssl-nginx` — dedicated OpenSSL 3.5 build for NGINX and Angie (kTLS offload, ec_nistp_64_gcc_128, RDRAND hardware entropy, OpenResty session yield patch, no legacy ciphers or bloat). See [deb.myguard.nl/?p=5210](https://deb.myguard.nl/?p=5210)
- **2026-05-07** NGINX: New modules
  - `libnginx-mod-http-aws-auth` — proxy requests to authenticated AWS services (Signature Version 4)
  - `libnginx-mod-http-cookie-flag` — set HttpOnly, Secure and SameSite flags on cookies
  - `libnginx-mod-http-memc` — Memcached ASCII protocol upstream module
  - `libnginx-mod-http-proxy-connect` — HTTP CONNECT tunneling through nginx
  - `libnginx-mod-http-push-stream` — pub/sub over HTTP long-polling, SSE and WebSocket
  - New patches:
    - `nginx-gzip-const-qualifier-fix.patch` — C99 const qualifier fix for the gzip filter; required for zlib-ng's stricter headers
    - `nginx_hpack.patch` — full HPACK response header compression for HTTP/2 (re-added to series)
    - `nginx-proxy-connect-1.29.patch` — patches the 1.29 core to add the parse states and request fields (`connect_host`, `connect_port`) that http-proxy-connect requires
- **2026-05-06** Refactoring package and docker build process, repo, sanitizing, testing
- **2026-05-04** Rebuild: NGINX 1.29.8
- **2026-05-04** Rebuild: ANGIE 1.11.4
- **2026-05-03** Adding support for Ubuntu 26.04 / Resolute. Refactoring some build scripts as well
- **2026-02-24** Rebuild: ANGIE 1.11.3
- **2026-02-24** Rebuild: NGINX 1.29.5
- **2026-02-24** Created a script to automatically convert the NGINX package to ANGIE for better compatibility and maintainability
- **2026-02-24** Probably going to trigger uploads for both NGINX and ANGIE

### 2025

- **2025-10-08** Release: NGINX 1.29.2
- **2025-09-28** Updated: [snuffleupagus](https://github.com/jvoisin/snuffleupagus) to 0.12.0 for trixie/bookworm/bullseye/noble/jammy and php 7.0/7.1/7.2/7.3/7.4/8.0/8.1/8.2/8.3/8.4
- **2025-09-25** Release: Angie 1.10.2
- **2025-09-25** Removed bionic and buster and old/stale/test repositories
- **2025-09-24** Fixed: package got stuck in Trixie publishing queue — thanks for noticing @theschappy
- **2025-09-22** Release: NGINX 1.29.1
- **2025-09-22** Computer temporarily fixed with duct tape and a PCH fan, building Docker images from tomorrow
- **2025-05-18** Rebuild Angie & NGINX, removed QUIC — it has been discontinued in April
- **2025-05-11** Rebuild: NGINX — added dependency version check on libmodsecurity3
- **2025-05-05** Rebuild: NGINX 1.28.0+quic, updated fork for zstd ([#20](https://github.com/eilandert/deb.myguard.nl/issues/20))
- **2025-04-27** Build: NGINX 1.28.0+quic, fixed faulty patch (dynamic_tls)
- **2025-02-25** Rebuild: NGINX 1.27.4+quic, fixed faulty patch in mod-security module (thanks for noticing @Arien02)

### 2024

- **2024-10-27** Rebuild: ANGIE 1.7.0+quic, some minor fixes in the transition from NGINX to Angie (@schories)
- **2024-10-22** Release: NGINX 1.27.2+quic
- **2024-10-22** Release: ANGIE 1.7.0+quic (removed Debian's `fix_pidfile.patch`)
- **2024-10-22** Added: new zlib-ng patch to work with zlib-ng 2.2.2
- **2024-10-22** Added: `ngx_dynamic_limit_req_module` in both nginx/angie and on the website
- **2024-07-06** Rebuild Angie/NGINX — fix for [issue #6](https://github.com/eilandert/deb.myguard.nl/issues/6)
- **2024-06-28** Release: ANGIE 1.6.0+quic
- **2024-06-02** Release: ANGIE 1.5.2+quic
- **2024-05-30** Release: NGINX 1.27.0+quic
- **2024-04-16** Release: NGINX 1.25.5+quic — the ssl-ct module breaks on it so that is disabled for now
- **2024-03-28** Release: ANGIE 1.5.0+quic with ACME support. See [angie.software/en/configuration/modules/http_acme/](https://angie.software/en/configuration/modules/http_acme/)
- **2024-02-15** Release: ANGIE 1.4.1+quic
- **2024-02-14** Release: NGINX Mainline 1.25.4+quic
- **2024-02-14** New modules upcoming: `http-length-hiding-filter` and `http-immutable` — for both Angie and NGINX
- **2024-01-14** Changed the Docker tag to `eilandert/nginx`
- **2024-01-01** Launched Angie in testing phase; this server is now running on [angie.software](https://angie.software/en/) for now — don't know if I'll keep supporting it yet
- **2024-01-01** Happy New Year

### 2023

- **2023-11-21** Updated build 1.25.3+quic, rebased on the Debian Trixie package
- **2023-11-17** Including new packages in a future build: `nginx-minimal`, `http-captcha`, `http-dynamic-etag`, `ipscrub`
- **2023-11-14** A build log is published at [raw.githubusercontent.com/eilandert/patches/main/nginx/nginx-build.log](https://raw.githubusercontent.com/eilandert/patches/main/nginx/nginx-build.log)
- **2023-11-13** Rebasing own stack onto the bookworm package to stay in sync with Debian/Ubuntu — in testing
- **2023-11-09** Official Pagespeed (*RETIRED*) documentation seems to be gone — new site: [pagespeed.myguard.nl](https://pagespeed.myguard.nl/)
- **2023-11-08** Updated build 1.25.3+quic including patches below
- **2023-11-08** Patched NGINX and OpenSSL to support yielding operations in `ssl_session_fetch_by_lua*` and `ssl_certificate_by_lua*`
- **2023-10-29** Updated build NGINX Mainline 1.25.3+quic
- **2023-10-28** New modules in the works for a new build: `set-misc-nginx-module`, `testcookie-nginx-module`, `xss-nginx-module`, `nginx-eval-module`, `nginx-http-user-agent`, `nginx-http-concat`, `nginx-access-plus`, `ngx_http_js_challenge_module`, `ngx_http_hmac_secure_link_module`, `headers-more-nginx-module`, `early-hints`, `flv-live`, `auth-ldap`
- **2023-10-27** Updated build 1.25.3+quic — updated brotli, got Bionic and Buster going again, fixed libjemalloc2, Pagespeed, ZSTD, changed default configs to the new nginx syntax
- **2023-10-24** Release: NGINX Mainline 1.25.3+quic
- **2023-10-20** Release: NGINX Mainline 1.25.2+quic, patched OpenSSL 3.0.x for QUIC/HTTP3 support (packages + Docker)
- **2023-06-13** Release: NGINX Mainline 1.25.1
- **2023-05-23** Release: NGINX Mainline 1.25.0

### 2022

- **2022-11-17** Release: 1.23.2 — brought back `http-sysguard` (removed previously due to compile errors)
- **2022-07-16** Release: 1.23.0 — improved NAXSI support, re-enabled PCRE2, new module `NGX_WAF`
- **2022-07-01** Release: NGINX 1.23.0 (mainline) — enabled pcre2 (while maintaining `-lpcre` for OpenResty lua)
- **2022-06-21** Delayed: NGINX Mainline 1.23.0 — waiting for fixes from OpenResty's lua and Pagespeed
- **2022-06-xx** Release: NGINX 1.22.0
- **2022-04-16** Rebuild NGINX and publish all changes from Edge (got tired of waiting for new NGINX release)
- **2022-01-25** Updated to NGINX 1.21.6 (upstream release)
- **2022-01-24** Rebuild NGINX and publish all changes
- **2022-01-06** Fixed a renaming issue with NAXSI (thanks to Tim Elston)
- **2022-01-01** Rebuild NGINX packages one more time to ensure sync after move to aptly
- **2022-01-01** Added `/etc/nginx/scripts/reorder-modules.sh` to deal with priorities and renaming
- **2022-01-01** Moved from reprepro to aptly (apt distribution)
- **2022-01-01** Happy New Year & start changelog

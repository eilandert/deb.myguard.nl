# deb.myguard.nl
issue tracker for the myguard packages on https://deb.myguard.nl

Created because my own forum got spammed.

NGINX/ANGIE CHANGELOG

2024-05-30 Release: NGINX 1.27.0+quic
2024-04-16 Release: NGINX 1.25.5+quic, the ssl-ct module breaks on it so that is disabled for now.
2024-03-28 Release: ANGIE 1.5.0+quic with ACME support. https://angie.software/en/configuration/modules/http_acme/
2024-02-15 Release: ANGIE 1.4.1+quic
2024-02-14 Release: NGINX Mainline 1.25.4+quic
2024-02-14 New modules upcoming:  http-length-hiding-filter and http-immutable.  For both Angie as NGINX.
2024-01-14 Changed the docker-tag to eilandert/nginx
2024-01-01 Launched Angie in testing phase, this server is now running on https://angie.software/en/ for now, don’t know if I keep supporting it yet.
2024-01-01 Happy New Year
2023-11-21 Updated build 1.25.3+quic, REBASED on the Debian Bookworm package
2023-11-17 Including new packages to a future build: nginx-minimal, http-captcha http-dynamic-etag, ipscrub
2023-11-14 A build log is published at https://raw.githubusercontent.com/eilandert/patches/main/nginx/nginx-build.log
2023-11-13 Rebasing my own stack onto the bookworm package to stay in sync with debian/ubuntu, in testing.
2023-11-09 Official Pagespeed (*RETIRED*) documentation seems to be gone, so here is a new site: https://pagespeed.myguard.nl/
2023-11-08 Updated build 1.25.3+quic including patches below
2023-11-08 Patched NGINX and OpenSSL in order to support yielding operations in ssl_session_fetch_by_lua* and ssl_certificate_by_lua*
2023-10-29 Updated build NGINX-Mainline 1.25.3+quic including packages below.
2023-10-28 New modules in the works for a new build: set-misc-nginx-module testcookie-nginx-module xss-nginx-module nginx-eval-module nginx-http-user-agent marxangels/nginx-http-concat nginx-access-plus ngx_http_js_challenge_module ngx_http_hmac_secure_link_module headers-more-nginx-module early-hints flv-live auth-ldap
2023-10-27 Updated build 1.25.3+quic, updated brotli, got Bionic and Buster going again, Fixed libjemalloc2, Pagespeed, ZSTD, changed default configs to the new nginx syntax
2023-10-24 Release: NGINX Mainline 1.25.3+quic
2023-10-20 Release: NGINX-Mainline 1.25.2+quic, patched OpenSSL3.0.x for QUIC/HTTP3 support. Packages+Dockers
2023-06-13 Release: NGINX Mainline 1.25.1
2023-05-23 Release:: NGINX Mainline 1.25.0
2022-11-17 Release: 1.23.2, brought back http-sysguard. Removed it before due to compile errors.
2022-07-16 Release: 1.23.0, given NAXSI some love, and renabling PCRE2, new module NGX_WAF
2022-07-01 Release: Published NGINX 1.23.0 (mainline), enabled pcre2 (while maintaining -lpcre for openresty lua)
2022-06-21 Delayed: NGINX Mainline (1.23.0), waiting for some fixes from e.g. openresty’s lua and pagespeed
2022-06-xx release: Published latest NGINX 1.22.0
2022-04-16 release: Rebuild NGINX and publish all changes from Edge. (got tired of waiting for new NGINX release)
2022-01-25 release: Updated to nginx 1.21.6 (upstream release)
2022-01-24 release: Rebuild NGINX and publish all changes below.
2022-01-06 release: Fixed a renaming issue with NAXSI (thanks to Tim Elston)
2022-01-01 release: Rebuild NGINX packages one more time in case something is not in sync due to the move to aptly
2022-01-01 release: added /etc/nginx/scripts/reorder-modules.sh to deal with priorities and renaming
2022-01-01 Moved from reprepro to aptly (apt distribition)
2022-01-01 Happy new year & start changelog

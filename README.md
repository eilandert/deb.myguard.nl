# deb.myguard.nl
issue tracker for the myguard packages on https://deb.myguard.nl

Created because my own forum got spammed.

NGINX/ANGIE CHANGELOG (only manually interventions are logged by default, automatic builds are not) <BR>
2025-04-27 build: NGINX-1.28.0+quic, fixed faulty patch (dynamic_tls)
2025-02-25 Rebuild: NGINX 1.27.4+quic, fixed faulty patch in mod-security module (thanks for noticing @Arien02) <BR>
2024-10-27 Rebuild: ANGIE 1.7.0+quic, some minor fixes in the transition from NGINX to Angie. (@schories) <BR>
2024-10-22 Release: NGINX 1.27.2+quic<BR>
2024-10-22 Release: ANGIE 1.7.0+quic (removed debians patch fix_pidfile.patch)<BR>
2024-10-22 Added: new zlib-ng patch to work with zlib-ng-2.2.2 version<BR>
2024-10-22 Added: ngx_dynamic_limit_req_module in both nginx/angie and on the website<BR>
2024-07-06 Rebuild Angie/NGINX for fix of https://github.com/eilandert/deb.myguard.nl/issues/6<BR>
2024-06-28 Release: ANGIE 1.6.0+quic<BR>
2024-06-02 Release: ANGIE 1.5.2+quic<BR>
2024-05-30 Release: NGINX 1.27.0+quic<BR>
2024-04-16 Release: NGINX 1.25.5+quic, the ssl-ct module breaks on it so that is disabled for now.<BR>
2024-03-28 Release: ANGIE 1.5.0+quic with ACME support. https://angie.software/en/configuration/modules/http_acme/<BR>
2024-02-15 Release: ANGIE 1.4.1+quic<BR>
2024-02-14 Release: NGINX Mainline 1.25.4+quic<BR>
2024-02-14 New modules upcoming:  http-length-hiding-filter and http-immutable.  For both Angie as NGINX.<BR>
2024-01-14 Changed the docker-tag to eilandert/nginx<BR>
2024-01-01 Launched Angie in testing phase, this server is now running on https://angie.software/en/ for now, don’t know if I keep supporting it yet.<BR>
2024-01-01 Happy New Year<BR>
2023-11-21 Updated build 1.25.3+quic, REBASED on the Debian Trixie package<BR>
2023-11-17 Including new packages to a future build: nginx-minimal, http-captcha http-dynamic-etag, ipscrub<BR>
2023-11-14 A build log is published at https://raw.githubusercontent.com/eilandert/patches/main/nginx/nginx-build.log<BR>
2023-11-13 Rebasing my own stack onto the bookworm package to stay in sync with debian/ubuntu, in testing.<BR>
2023-11-09 Official Pagespeed (*RETIRED*) documentation seems to be gone, so here is a new site: https://pagespeed.myguard.nl/<BR>
2023-11-08 Updated build 1.25.3+quic including patches below<BR>
2023-11-08 Patched NGINX and OpenSSL in order to support yielding operations in ssl_session_fetch_by_lua* and ssl_certificate_by_lua*<BR>
2023-10-29 Updated build NGINX-Mainline 1.25.3+quic including packages below.<BR>
2023-10-28 New modules in the works for a new build: set-misc-nginx-module testcookie-nginx-module xss-nginx-module nginx-eval-module nginx-http-user-agent marxangels/nginx-http-concat nginx-access-plus ngx_http_js_challenge_module ngx_http_hmac_secure_link_module headers-more-nginx-module early-hints flv-live auth-ldap<BR>
2023-10-27 Updated build 1.25.3+quic, updated brotli, got Bionic and Buster going again, Fixed libjemalloc2, Pagespeed, ZSTD, changed default configs to the new nginx syntax<BR>
2023-10-24 Release: NGINX Mainline 1.25.3+quic<BR>
2023-10-20 Release: NGINX-Mainline 1.25.2+quic, patched OpenSSL3.0.x for QUIC/HTTP3 support. Packages+Dockers<BR>
2023-06-13 Release: NGINX Mainline 1.25.1<BR>
2023-05-23 Release:: NGINX Mainline 1.25.0<BR>
2022-11-17 Release: 1.23.2, brought back http-sysguard. Removed it before due to compile errors.<BR>
2022-07-16 Release: 1.23.0, given NAXSI some love, and renabling PCRE2, new module NGX_WAF<BR>
2022-07-01 Release: Published NGINX 1.23.0 (mainline), enabled pcre2 (while maintaining -lpcre for openresty lua)<BR>
2022-06-21 Delayed: NGINX Mainline (1.23.0), waiting for some fixes from e.g. openresty’s lua and pagespeed<BR>
2022-06-xx release: Published latest NGINX 1.22.0<BR>
2022-04-16 release: Rebuild NGINX and publish all changes from Edge. (got tired of waiting for new NGINX release)<BR>
2022-01-25 release: Updated to nginx 1.21.6 (upstream release)<BR>
2022-01-24 release: Rebuild NGINX and publish all changes below.<BR>
2022-01-06 release: Fixed a renaming issue with NAXSI (thanks to Tim Elston)<BR>
2022-01-01 release: Rebuild NGINX packages one more time in case something is not in sync due to the move to aptly<BR>
2022-01-01 release: added /etc/nginx/scripts/reorder-modules.sh to deal with priorities and renaming<BR>
2022-01-01 Moved from reprepro to aptly (apt distribition)<BR>
2022-01-01 Happy new year & start changelog<BR>

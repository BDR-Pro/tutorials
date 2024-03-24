# Networking TCP Sequence Diagram

This block represents a sequence of networking operations performed by a client to access a webpage, specifically GitHub, using the Curl command. It showcases the intricacies of establishing a secure HTTP connection, sending HTTP requests, and handling responses. Here's a breakdown of what's happening:

1. **Connecting to the Server:**
   - `Trying 20.233.83.145:443...`: The client attempts to establish a TCP connection to the server at the IP address `20.233.83.145` on port `443`, which is the standard port for HTTPS.
   - `Connected to github.com (20.233.83.145) port 443`: The TCP connection is successfully established.

2. **SSL/TLS Handshake:**
   - `schannel: disabled automatic use of client certificate`: Indicates the Secure Channel (Schannel) security package is not using a client certificate automatically. Schannel is a Security Support Provider (SSP) that implements the SSL, TLS, and DTLS Internet standard authentication protocols.
   - The client and server perform a series of messages to negotiate the cryptographic algorithms, exchange keys, and establish a secure encrypted connection. This process is not detailed but involves steps like `schannel: renegotiating SSL/TLS connection` and mentions of ALPN (Application-Layer Protocol Negotiation) where the client proposes using HTTP/1.1.

3. **HTTP Request:**
   - The client sends an HTTP GET request to the server. This request includes headers like `Host: github.com`, indicating the domain being accessed, and `User-Agent`, specifying the client software making the request.

4. **Server Response:**
   - The server responds with various headers, including `HTTP/1.1 200 OK`, signifying a successful response. Other response headers include `Server: GitHub.com`, indicating the server software, and various security headers like `Strict-Transport-Security`, which enforces secure connections, and `Content-Security-Policy`, defining what resources the browser is allowed to load for the page.
   - `Set-Cookie` headers are used to set cookies in the client's browser, which can be used for maintaining session state or tracking.

5. **Content Delivery:**
   - The `Content-Security-Policy` header is particularly long, showcasing GitHub's extensive policy for controlling resources the page can request or execute, enhancing security.
   - The response includes HTML content (not fully detailed here) that the client's web browser would render into the webpage the user sees. This content is received in chunks, as indicated by `Recv data`.

6. **Encryption Details:**
   - There are multiple mentions of renegotiating the SSL/TLS connection, which might involve updating the encryption parameters. Also, messages like `schannel: failed to decrypt data, need more data` suggest the complexities involved in securely transmitting data.

7. **Conclusion:**
   - This sequence demonstrates a typical flow of HTTPS communication: establishing a secure connection, exchanging HTTP requests and responses, and finally rendering the server's response as a webpage. It underscores the multiple layers of security and efficiency optimizations (like ALPN) involved in modern web browsing.

---

```bash

== Info:   Trying 20.233.83.145:443...
== Info: Connected to github.com (20.233.83.145) port 443
== Info: schannel: disabled automatic use of client certificate
== Info: ALPN: curl offers http/1.1
== Info: ALPN: server accepted http/1.1
== Info: using HTTP/1.1
=> Send header, 73 bytes (0x49)
0000: GET / HTTP/1.1
0010: Host: github.com
0022: User-Agent: curl/8.4.0
003a: Accept: */*
0047: 
== Info: schannel: remote party requests renegotiation
== Info: schannel: renegotiating SSL/TLS connection
== Info: schannel: SSL/TLS connection renegotiated
== Info: schannel: remote party requests renegotiation
== Info: schannel: renegotiating SSL/TLS connection
== Info: schannel: SSL/TLS connection renegotiated
== Info: schannel: failed to decrypt data, need more data
<= Recv header, 17 bytes (0x11)
0000: HTTP/1.1 200 OK
<= Recv header, 20 bytes (0x14)
0000: Server: GitHub.com
<= Recv header, 37 bytes (0x25)
0000: Date: Sun, 24 Mar 2024 16:09:10 GMT
<= Recv header, 40 bytes (0x28)
0000: Content-Type: text/html; charset=utf-8
<= Recv header, 118 bytes (0x76)
0000: Vary: X-PJAX, X-PJAX-Container, Turbo-Visit, Turbo-Frame, Accept
0040: -Language, Accept-Encoding, Accept, X-Requested-With
<= Recv header, 25 bytes (0x19)
0000: content-language: en-US
<= Recv header, 44 bytes (0x2c)
0000: ETag: W/"cb59bd821adefbff09885fbc6e28b663"
<= Recv header, 52 bytes (0x34)
0000: Cache-Control: max-age=0, private, must-revalidate
<= Recv header, 73 bytes (0x49)
0000: Strict-Transport-Security: max-age=31536000; includeSubdomains; 
0040: preload
<= Recv header, 23 bytes (0x17)
0000: X-Frame-Options: deny
<= Recv header, 33 bytes (0x21)
0000: X-Content-Type-Options: nosniff
<= Recv header, 21 bytes (0x15)
0000: X-XSS-Protection: 0
<= Recv header, 76 bytes (0x4c)
0000: Referrer-Policy: origin-when-cross-origin, strict-origin-when-cr
0040: oss-origin
<= Recv header, 2864 bytes (0xb30)
0000: Content-Security-Policy: default-src 'none'; base-uri 'self'; ch
0040: ild-src github.com/assets-cdn/worker/ gist.github.com/assets-cdn
0080: /worker/; connect-src 'self' uploads.github.com www.githubstatus
00c0: .com collector.github.com raw.githubusercontent.com api.github.c
0100: om github-cloud.s3.amazonaws.com github-production-repository-fi
0140: le-5c1aeb.s3.amazonaws.com github-production-upload-manifest-fil
0180: e-7fdce7.s3.amazonaws.com github-production-user-asset-6210df.s3
01c0: .amazonaws.com api.githubcopilot.com objects-origin.githubuserco
0200: ntent.com *.actions.githubusercontent.com wss://*.actions.github
0240: usercontent.com productionresultssa0.blob.core.windows.net/ prod
0280: uctionresultssa1.blob.core.windows.net/ productionresultssa2.blo
02c0: b.core.windows.net/ productionresultssa3.blob.core.windows.net/ 
0300: productionresultssa4.blob.core.windows.net/ productionresultssa5
0340: .blob.core.windows.net/ productionresultssa6.blob.core.windows.n
0380: et/ productionresultssa7.blob.core.windows.net/ productionresult
03c0: ssa8.blob.core.windows.net/ productionresultssa9.blob.core.windo
0400: ws.net/ productionresultssa10.blob.core.windows.net/ productionr
0440: esultssa11.blob.core.windows.net/ productionresultssa12.blob.cor
0480: e.windows.net/ productionresultssa13.blob.core.windows.net/ prod
04c0: uctionresultssa14.blob.core.windows.net/ productionresultssa15.b
0500: lob.core.windows.net/ productionresultssa16.blob.core.windows.ne
0540: t/ productionresultssa17.blob.core.windows.net/ productionresult
0580: ssa18.blob.core.windows.net/ productionresultssa19.blob.core.win
05c0: dows.net/ github-production-repository-image-32fea6.s3.amazonaws
0600: .com github-production-release-asset-2e65be.s3.amazonaws.com ins
0640: ights.github.com wss://alive.github.com github.githubassets.com;
0680:  font-src github.githubassets.com; form-action 'self' github.com
06c0:  gist.github.com objects-origin.githubusercontent.com; frame-anc
0700: estors 'none'; frame-src viewscreen.githubusercontent.com notebo
0740: oks.githubusercontent.com; img-src 'self' data: github.githubass
0780: ets.com media.githubusercontent.com camo.githubusercontent.com i
07c0: denticons.github.com avatars.githubusercontent.com github-cloud.
0800: s3.amazonaws.com objects.githubusercontent.com secured-user-imag
0840: es.githubusercontent.com/ user-images.githubusercontent.com/ pri
0880: vate-user-images.githubusercontent.com opengraph.githubassets.co
08c0: m github-production-user-asset-6210df.s3.amazonaws.com customer-
0900: stories-feed.github.com spotlights-feed.github.com objects-origi
0940: n.githubusercontent.com *.githubusercontent.com; manifest-src 's
0980: elf'; media-src github.com user-images.githubusercontent.com/ se
09c0: cured-user-images.githubusercontent.com/ private-user-images.git
0a00: hubusercontent.com github-production-user-asset-6210df.s3.amazon
0a40: aws.com gist.github.com github.githubassets.com; script-src gith
0a80: ub.githubassets.com; style-src 'unsafe-inline' github.githubasse
0ac0: ts.com; upgrade-insecure-requests; worker-src github.com/assets-
0b00: cdn/worker/ gist.github.com/assets-cdn/worker/
<= Recv header, 423 bytes (0x1a7)
0000: Set-Cookie: _gh_sess=HPsBgMo%2B1vGSjE%2BhrP%2FYPwckfpDbwlhtjF8d3
0040: mwo4HAihWujVJlRITXNST26MK7Yqb0OZzyJyOtDrIOEl3In71vI947%2FoPSuKAr
0080: 56TGTyOmQjbfpROeXNExs8W0kCY9KqL4%2F6lPYuHpdn%2FxfFD0J7QkWSIeMPo%
00c0: 2Bky%2FUOU3oFvNjQbvA1JUeugR5cFh0xCyxlnf71d4aBak3QSPUDesDrARwOiJX
0100: NTn2flBM%2Fo5lu4GpdRje%2F4gOxUj4XJMv%2FYlkGeqcACSDyLMpg%2F4h%2FO
0140: eyZgA%3D%3D--3l3KWXJColf36p2Y--H%2Frb8pDchJO5IiKa7fUrUA%3D%3D; P
0180: ath=/; HttpOnly; Secure; SameSite=Lax
<= Recv header, 135 bytes (0x87)
0000: Set-Cookie: _octo=GH1.1.2011737728.1711296550; Path=/; Domain=gi
0040: thub.com; Expires=Mon, 24 Mar 2025 16:09:10 GMT; Secure; SameSit
0080: e=Lax
<= Recv header, 124 bytes (0x7c)
0000: Set-Cookie: logged_in=no; Path=/; Domain=github.com; Expires=Mon
0040: , 24 Mar 2025 16:09:10 GMT; HttpOnly; Secure; SameSite=Lax
<= Recv header, 22 bytes (0x16)
0000: Accept-Ranges: bytes
<= Recv header, 28 bytes (0x1c)
0000: Transfer-Encoding: chunked
<= Recv header, 57 bytes (0x39)
0000: X-GitHub-Request-Id: CB23:273E92:165FA2:251059:66005026
<= Recv header, 2 bytes (0x2)
0000: 
<= Recv data, 6850 bytes (0x1ac2)
0000: 1B46
0006: ......<!DOCTYPE html>.<html.  lang="en".  .  .  data-a11y-animat
0046: ed-images="system" data-a11y-link-underlines="true".  >.....  <h
0086: ead>.    <meta charset="utf-8">.  <link rel="dns-prefetch" href=
00c6: "https://github.githubassets.com">.  <link rel="dns-prefetch" hr
0106: ef="https://avatars.githubusercontent.com">.  <link rel="dns-pre
0146: fetch" href="https://github-cloud.s3.amazonaws.com">.  <link rel
0186: ="dns-prefetch" href="https://user-images.githubusercontent.com/
01c6: ">.  <link rel="preconnect" href="https://github.githubassets.co
0206: m" crossorigin>.  <link rel="preconnect" href="https://avatars.g
0246: ithubusercontent.com">..  ..  <link crossorigin="anonymous" medi
0286: a="all" rel="stylesheet" href="https://github.githubassets.com/a
02c6: ssets/light-0eace2597ca3.css" /><link crossorigin="anonymous" me
0306: dia="all" rel="stylesheet" href="https://github.githubassets.com
0346: /assets/dark-a167e256da9c.css" /><link data-color-theme="light" 
0386: crossorigin="anonymous" media="all" rel="stylesheet" data-href="
03c6: https://github.githubassets.com/assets/light-0eace2597ca3.css" /
0406: ><link data-color-theme="dark" crossorigin="anonymous" media="al
0446: l" rel="stylesheet" data-href="https://github.githubassets.com/a
0486: ssets/dark-a167e256da9c.css" /><link data-color-theme="dark_dimm
04c6: ed" crossorigin="anonymous" media="all" rel="stylesheet" data-hr
0506: ef="https://github.githubassets.com/assets/dark_dimmed-d11f2cf80
0546: 09b.css" /><link data-color-theme="dark_high_contrast" crossorig
0586: in="anonymous" media="all" rel="stylesheet" data-href="https://g
05c6: ithub.githubassets.com/assets/dark_high_contrast-ea7373db06c8.cs
0606: s" /><link data-color-theme="dark_colorblind" crossorigin="anony
0646: mous" media="all" rel="stylesheet" data-href="https://github.git
0686: hubassets.com/assets/dark_colorblind-afa99dcf40f7.css" /><link d
06c6: ata-color-theme="light_colorblind" crossorigin="anonymous" media
0706: ="all" rel="stylesheet" data-href="https://github.githubassets.c
0746: om/assets/light_colorblind-af6c685139ba.css" /><link data-color-
0786: theme="light_high_contrast" crossorigin="anonymous" media="all" 
07c6: rel="stylesheet" data-href="https://github.githubassets.com/asse
0806: ts/light_high_contrast-578cdbc8a5a9.css" /><link data-color-them
0846: e="light_tritanopia" crossorigin="anonymous" media="all" rel="st
0886: ylesheet" data-href="https://github.githubassets.com/assets/ligh
08c6: t_tritanopia-5cb699a7e247.css" /><link data-color-theme="dark_tr
0906: itanopia" crossorigin="anonymous" media="all" rel="stylesheet" d
0946: ata-href="https://github.githubassets.com/assets/dark_tritanopia
0986: -9b32204967c6.css" />.    <link crossorigin="anonymous" media="a
09c6: ll" rel="stylesheet" href="https://github.githubassets.com/asset
0a06: s/primer-primitives-366b5c973fad.css" />.    <link crossorigin="
0a46: anonymous" media="all" rel="stylesheet" href="https://github.git
0a86: hubassets.com/assets/primer-f3607eccaaae.css" />.    <link cross
0ac6: origin="anonymous" media="all" rel="stylesheet" href="https://gi
0b06: thub.githubassets.com/assets/global-c2f8efb9bce8.css" />.    <li
0b46: nk crossorigin="anonymous" media="all" rel="stylesheet" href="ht
0b86: tps://github.githubassets.com/assets/github-19c85be4af9c.css" />
0bc6: .  <link crossorigin="anonymous" media="all" rel="stylesheet" hr
0c06: ef="https://github.githubassets.com/assets/dashboard-eff64098065
0c46: 0.css" />.<link crossorigin="anonymous" media="all" rel="stylesh
0c86: eet" href="https://github.githubassets.com/assets/discussions-4a
0cc6: 9715cdd9f3.css" />.<link crossorigin="anonymous" media="all" rel
0d06: ="stylesheet" href="https://github.githubassets.com/assets/site-
0d46: 5c3e54ae0543.css" />.<link crossorigin="anonymous" media="all" r
0d86: el="stylesheet" href="https://github.githubassets.com/assets/hom
0dc6: e-bd387065bbce.css" />..  ...  <script type="application/json" i
0e06: d="client-env">{"locale":"en","featureFlags":["code_vulnerabilit
0e46: y_scanning","copilot_conversational_ux_history_refs","copilot_sm
0e86: ell_icebreaker_ux","copilot_implicit_context","failbot_handle_no
0ec6: n_errors","geojson_azure_maps","image_metric_tracking","marketin
0f06: g_forms_api_integration_contact_request","marketing_pages_search
0f46: _explore_provider","turbo_experiment_risky","sample_network_conn
0f86: _type","no_character_key_shortcuts_in_inputs","react_start_trans
0fc6: ition_for_navigations","custom_inp","remove_child_patch","site_f
1006: eatures_copilot_cli_ga","copilot_code_chat_diff_header_button"]}
1046: </script>.<script crossorigin="anonymous" defer="defer" type="ap
1086: plication/javascript" src="https://github.githubassets.com/asset
10c6: s/wp-runtime-9e5505a38c86.js"></script>.<script crossorigin="ano
1106: nymous" defer="defer" type="application/javascript" src="https:/
1146: /github.githubassets.com/assets/vendors-node_modules_dompurify_d
1186: ist_purify_js-6890e890956f.js"></script>.<script crossorigin="an
11c6: onymous" defer="defer" type="application/javascript" src="https:
1206: //github.githubassets.com/assets/vendors-node_modules_stacktrace
1246: -parser_dist_stack-trace-parser_esm_js-node_modules_github_bro-a
1286: 4c183-79f9611c275b.js"></script>.<script crossorigin="anonymous"
12c6:  defer="defer" type="application/javascript" src="https://github
1306: .githubassets.com/assets/vendors-node_modules_oddbird_popover-po
1346: lyfill_dist_popover_js-7bd350d761f4.js"></script>.<script crosso
1386: rigin="anonymous" defer="defer" type="application/javascript" sr
13c6: c="https://github.githubassets.com/assets/ui_packages_failbot_fa
1406: ilbot_ts-5bd9ba639cc0.js"></script>.<script crossorigin="anonymo
1446: us" defer="defer" type="application/javascript" src="https://git
1486: hub.githubassets.com/assets/environment-27057bd9ed0b.js"></scrip
14c6: t>.<script crossorigin="anonymous" defer="defer" type="applicati
1506: on/javascript" src="https://github.githubassets.com/assets/vendo
1546: rs-node_modules_github_selector-observer_dist_index_esm_js-9f960
1586: d9b217c.js"></script>.<script crossorigin="anonymous" defer="def
15c6: er" type="application/javascript" src="https://github.githubasse
1606: ts.com/assets/vendors-node_modules_primer_behaviors_dist_esm_foc
1646: us-zone_js-086f7a27bac0.js"></script>.<script crossorigin="anony
1686: mous" defer="defer" type="application/javascript" src="https://g
16c6: ithub.githubassets.com/assets/vendors-node_modules_github_relati
1706: ve-time-element_dist_index_js-c76945c5961a.js"></script>.<script
1746:  crossorigin="anonymous" defer="defer" type="application/javascr
1786: ipt" src="https://github.githubassets.com/assets/vendors-node_mo
17c6: dules_github_combobox-nav_dist_index_js-node_modules_github_mark
1806: down-toolbar-e-820fc0-bc8f02b96749.js"></script>.<script crossor
1846: igin="anonymous" defer="defer" type="application/javascript" src
1886: ="https://github.githubassets.com/assets/vendors-node_modules_de
18c6: legated-events_dist_index_js-node_modules_github_auto-complete-e
1906: lement-81d69b-d1813ba335d8.js"></script>.<script crossorigin="an
1946: onymous" defer="defer" type="application/javascript" src="https:
1986: //github.githubassets.com/assets/vendors-node_modules_github_tex
19c6: t-expander-element_dist_index_js-8a621df59e80.js"></script>.<scr
1a06: ipt crossorigin="anonymous" defer="defer" type="application/java
1a46: script" src="https://github.githubassets.com/assets/vendors-node
1a86: _modules_github_filter-input-element_dist_index_js-node_modu
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 1510 bytes (0x5e6)
0000: les_github_remote-inp-b7d8f4-654130b7cde5.js"></script>.<script 
0040: crossorigin="anonymous" defer="defer" type="application/javascri
0080: pt" src="h
008c: 1B4E
0092: ttps://github.githubassets.com/assets/vendors-node_modules_githu
00d2: b_file-attachment-element_dist_index_js-node_modules_primer_view
0112: -co-3959a9-68b3d6c8feb2.js"></script>.<script crossorigin="anony
0152: mous" defer="defer" type="application/javascript" src="https://g
0192: ithub.githubassets.com/assets/github-elements-369bd99876f6.js"><
01d2: /script>.<script crossorigin="anonymous" defer="defer" type="app
0212: lication/javascript" src="https://github.githubassets.com/assets
0252: /element-registry-fb4b8d40f206.js"></script>.<script crossorigin
0292: ="anonymous" defer="defer" type="application/javascript" src="ht
02d2: tps://github.githubassets.com/assets/vendors-node_modules_github
0312: _mini-throttle_dist_index_js-node_modules_github_alive-client_di
0352: st-bf5aa2-5a0e291a0298.js"></script>.<script crossorigin="anonym
0392: ous" defer="defer" type="application/javascript" src="https://gi
03d2: thub.githubassets.com/assets/vendors-node_modules_lit-html_lit-h
0412: tml_js-5b376145beff.js"></script>.<script crossorigin="anonymous
0452: " defer="defer" type="application/javascript" src="https://githu
0492: b.githubassets.com/assets/vendors-node_modules_morphdom_dist_mor
04d2: phdom-esm_js-5bff297a06de.js"></script>.<script crossorigin="ano
0512: nymous" defer="defer" type="application/javascript" src="https:/
0552: /github.githubassets.com/assets/vendors-node_modules_github_turb
0592: o_dist_turbo_es2017-esm_js-c91f4ad18b62.js"></script>.<script cr
05d2: ossorigin="anonymous
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 6998 bytes (0x1b56)
0000: " defer="defer" type="application/javascript" src="https://githu
0040: b.githubassets.com/assets/vendors-node_modules_github_remote-for
0080: m_dist_index_js-node_modules_scroll-anchoring_dist_scro-52dc4b-4
00c0: fecca2d00e4.js"></script>.<script crossorigin="anonymous" defer=
0100: "defer" type="application/javascript" src="https://github.github
0140: assets.com/assets/vendors-node_modules_color-convert_index_js-72
0180: c9fbde5ad4.js"></script>.<script crossorigin="anonymous" defer="
01c0: defer" type="application/javascript" src="https://github.githuba
0200: ssets.com/assets/vendors-node_modules_primer_behaviors_dist_esm_
0240: dimensions_js-node_modules_github_jtml_lib_index_js-95b84ee6bc34
0280: .js"></script>.<script crossorigin="anonymous" defer="defer" typ
02c0: e="application/javascript" src="https://github.githubassets.com/
0300: assets/vendors-node_modules_github_paste-markdown_dist_index_esm
0340: _js-node_modules_github_quote-select-cbac5f-c7885f4526c5.js"></s
0380: cript>.<script crossorigin="anonymous" defer="defer" type="appli
03c0: cation/javascript" src="https://github.githubassets.com/assets/a
0400: pp_assets_modules_github_updatable-content_ts-ee3fc84d7fb0.js"><
0440: /script>.<script crossorigin="anonymous" defer="defer" type="app
0480: lication/javascript" src="https://github.githubassets.com/assets
04c0: /app_assets_modules_github_behaviors_task-list_ts-app_assets_mod
0500: ules_github_onfocus_ts-app_ass-421cec-9de4213015af.js"></script>
0540: .<script crossorigin="anonymous" defer="defer" type="application
0580: /javascript" src="https://github.githubassets.com/assets/app_ass
05c0: ets_modules_github_sticky-scroll-into-view_ts-94209c43e6af.js"><
0600: /script>.<script crossorigin="anonymous" defer="defer" type="app
0640: lication/javascript" src="https://github.githubassets.com/assets
0680: /app_assets_modules_github_behaviors_ajax-error_ts-app_assets_mo
06c0: dules_github_behaviors_include-467754-244ee9d9ed77.js"></script>
0700: .<script crossorigin="anonymous" defer="defer" type="application
0740: /javascript" src="https://github.githubassets.com/assets/app_ass
0780: ets_modules_github_behaviors_commenting_edit_ts-app_assets_modul
07c0: es_github_behaviors_ht-83c235-9285faa0e011.js"></script>.<script
0800:  crossorigin="anonymous" defer="defer" type="application/javascr
0840: ipt" src="https://github.githubassets.com/assets/behaviors-4e25e
0880: 265ef84.js"></script>.<script crossorigin="anonymous" defer="def
08c0: er" type="application/javascript" src="https://github.githubasse
0900: ts.com/assets/vendors-node_modules_delegated-events_dist_index_j
0940: s-node_modules_github_catalyst_lib_index_js-d0256ebff5cd.js"></s
0980: cript>.<script crossorigin="anonymous" defer="defer" type="appli
09c0: cation/javascript" src="https://github.githubassets.com/assets/n
0a00: otifications-global-352d84c6cc82.js"></script>.<script crossorig
0a40: in="anonymous" defer="defer" type="application/javascript" src="
0a80: https://github.githubassets.com/assets/vendors-node_modules_dele
0ac0: gated-events_dist_index_js-node_modules_github_catalyst_lib_inde
0b00: x_js-b4a243-ee680693e2b9.js"></script>.<script crossorigin="anon
0b40: ymous" defer="defer" type="application/javascript" src="https://
0b80: github.githubassets.com/assets/marketing-0f9641faa97a.js"></scri
0bc0: pt>.<script crossorigin="anonymous" defer="defer" type="applicat
0c00: ion/javascript" src="https://github.githubassets.com/assets/home
0c40: -b79d63e9f100.js"></script>.<script crossorigin="anonymous" defe
0c80: r="defer" type="application/javascript" src="https://github.gith
0cc0: ubassets.com/assets/vendors-node_modules_github_webgl-globe_dist
0d00: _js_main_js-cf5f119d1214.js"></script>.<script crossorigin="anon
0d40: ymous" defer="defer" type="application/javascript" src="https://
0d80: github.githubassets.com/assets/webgl-globe-d3e3295f0ac2.js"></sc
0dc0: ript>.  ..  <title>GitHub: Let...s build from here .. GitHub</ti
0e00: tle>....  <meta name="route-pattern" content="/" data-turbo-tran
0e40: sient>.  <meta name="route-controller" content="dashboard" data-
0e80: turbo-transient>.  <meta name="route-action" content="index" dat
0ec0: a-turbo-transient>..    .  <meta name="current-catalog-service-h
0f00: ash" content="40dc28bd654b20f337468a532ff456ed5863889cfbb4e982b7
0f40: 93597321d48d3f">...  <meta name="request-id" content="CB23:273E9
0f80: 2:165FA2:251059:66005026" data-pjax-transient="true"/><meta name
0fc0: ="html-safe-nonce" content="dc1e0db85956840611e3b3fe80778eeb337e
1000: ef9a0ce462a9f4f8a77dabe4d65f" data-pjax-transient="true"/><meta 
1040: name="visitor-payload" content="eyJyZWZlcnJlciI6IiIsInJlcXVlc3Rf
1080: aWQiOiJDQjIzOjI3M0U5MjoxNjVGQTI6MjUxMDU5OjY2MDA1MDI2IiwidmlzaXRv
10c0: cl9pZCI6Ijg2NDAzNDc3NTE2MDA2NDAwMzgiLCJyZWdpb25fZWRnZSI6InVhZW5v
1100: cnRoIiwicmVnaW9uX3JlbmRlciI6InVhZW5vcnRoIn0=" data-pjax-transien
1140: t="true"/><meta name="visitor-hmac" content="c71da171458c6d96f41
1180: b34797fedc28752d6353d6d288f6c346c782e22792a5b" data-pjax-transie
11c0: nt="true"/>....    <meta name="page-subject" content="GitHub">..
1200:   <meta name="github-keyboard-shortcuts" content="dashboards,cop
1240: ilot" data-turbo-transient="true" />.  ..  <meta name="selected-
1280: link" value="/" data-turbo-transient>.  <link rel="assets" href=
12c0: "https://github.githubassets.com/">..    <meta name="google-site
1300: -verification" content="c1kuD-K2HIVF635lypcsWPoD4kilo5-jA_wBFyT4
1340: uMY">.  <meta name="google-site-verification" content="KT5gs8h0w
1380: vaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">.  <meta name="google-site-v
13c0: erification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fs
1400: A">.  <meta name="google-site-verification" content="GXs5KoUUkNC
1440: oaAZn7wPN-t01Pywp9M3sEjnt_3_ZWPc">.  <meta name="google-site-ver
1480: ification" content="Apib7-x98H0j5cPqHWwSMm6dNU4GmODRoqxLiDzdx9I"
14c0: >..<meta name="octolytics-url" content="https://collector.github
1500: .com/github/collect" />..  ..  ......    <meta name="user-login"
1540:  content="">..  ..    <meta name="viewport" content="width=devic
1580: e-width">.    .      <meta name="description" content="GitHub is
15c0:  where over 100 million developers shape the future of sof
15fc: 263A
1602: tware, together. Contribute to the open source community, manage
1642:  your Git repositories, review code like a pro, track bugs and f
1682: eatures, power your CI/CD and DevOps workflows, and secure code 
16c2: before you commit it.">.      <link rel="search" type="applicati
1702: on/opensearchdescription+xml" href="/opensearch.xml" title="GitH
1742: ub">.    <link rel="fluid-icon" href="https://github.com/fluidic
1782: on.png" title="GitHub">.    <meta property="fb:app_id" content="
17c2: 1401488693436528">.    <meta name="apple-itunes-app" content="ap
1802: p-id=1477376905, app-argument=https://github.com/" />.      <met
1842: a name="twitter:image:src" content="https://github.githubassets.
1882: com/assets/campaign-social-031d6161fa10.png" /><meta name="twitt
18c2: er:site" content="@github" /><meta name="twitter:card" content="
1902: summary_large_image" /><meta name="twitter:title" content="GitHu
1942: b: Let...s build from here" /><meta name="twitter:description" c
1982: ontent="GitHub is where over 100 million developers shape the fu
19c2: ture of software, together. Contribute to the open source commun
1a02: ity, manage your Git repositories, review code like a pro, track
1a42:  bugs and fea..." />.      <meta property="og:image" content="ht
1a82: tps://github.githubassets.com/assets/campaign-social-031d6161fa1
1ac2: 0.png" /><meta property="og:image:alt" content="GitHub is where 
1b02: over 100 million developers shape the future of software, togeth
1b42: er. Contribute to th
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 15274 bytes (0x3baa)
0000: e open source community, manage your Git repositories, review co
0040: de like a pro, track bugs and fea..." /><meta property="og:site_
0080: name" content="GitHub" /><meta property="og:type" content="objec
00c0: t" /><meta property="og:title" content="GitHub: Let...s build fr
0100: om here" /><meta property="og:url" content="https://github.com/"
0140:  /><meta property="og:description" content="GitHub is where over
0180:  100 million developers shape the future of software, together. 
01c0: Contribute to the open source community, manage your Git reposit
0200: ories, review code like a pro, track bugs and fea..." />.      .
0240: ...        <meta name="hostname" content="github.com">....      
0280:   <meta name="expected-hostname" content="github.com">...  <meta
02c0:  http-equiv="x-pjax-version" content="bf19614ff8d2120db4b447ab9d
0300: 02d7ed663fa0cb881fecb2e420b1b7c18dba7a" data-turbo-track="reload
0340: ">.  <meta http-equiv="x-pjax-csp-version" content="6b606b69d609
0380: bde981b31b4b202bffac943c25f9230dd7f78c45cb5beb91012e" data-turbo
03c0: -track="reload">.  <meta http-equiv="x-pjax-css-version" content
0400: ="4ed2df85e436c9302f86ff3fcd9d18714ca3fbadabc250472f3d50e7da2380
0440: 83" data-turbo-track="reload">.  <meta http-equiv="x-pjax-js-ver
0480: sion" content="3d9d83272430fb6954066beb575ce5dad9c7e8f7847204760
04c0: 67f4f0f1c23c6c8" data-turbo-track="reload">..  <meta name="turbo
0500: -cache-control" content="no-preview" data-turbo-transient="">.. 
0540:      <meta property="og:image:type" content="image/png">.  <meta
0580:  property="og:image:width" content="1200">.  <meta property="og:
05c0: image:height" content="630">..  <link rel="me" href="https://hac
0600: hyderm.io/@github">..  <link crossorigin="anonymous" media="all"
0640:  rel="stylesheet" href="https://github.githubassets.com/assets/h
0680: ome-bd387065bbce.css" />.  <link rel="preload" href="https://git
06c0: hub.githubassets.com/assets/mona-sans-d1bf285e9b9b.woff2" as="fo
0700: nt" type="font/woff2" crossorigin>.  <meta name="is_logged_out_p
0740: age" content="true">....    <link rel="canonical" href="https://
0780: github.com/" data-turbo-transient>.  <meta name="turbo-body-clas
07c0: ses" content="logged-out env-production page-responsive header-o
0800: verlay home-campaign">...  <meta name="browser-stats-url" conten
0840: t="https://api.github.com/_private/browser/stats">..  <meta name
0880: ="browser-errors-url" content="https://api.github.com/_private/b
08c0: rowser/errors">..  <link rel="mask-icon" href="https://github.gi
0900: thubassets.com/assets/pinned-octocat-093da3e6fa40.svg" color="#0
0940: 00000">.  <link rel="alternate icon" class="js-site-favicon" typ
0980: e="image/png" href="https://github.githubassets.com/favicons/fav
09c0: icon.png">.  <link rel="icon" class="js-site-favicon" type="imag
0a00: e/svg+xml" href="https://github.githubassets.com/favicons/favico
0a40: n.svg">..<meta name="theme-color" content="#1e2327">....  <link 
0a80: rel="manifest" href="/manifest.json" crossOrigin="use-credential
0ac0: s">..  </head>..  <body class="logged-out env-production page-re
0b00: sponsive header-overlay home-campaign" style="word-wrap: break-w
0b40: ord;">.    <div data-turbo-body class="logged-out env-production
0b80:  page-responsive header-overlay home-campaign" style="word-wrap:
0bc0:  break-word;">.      ...    <div class="position-relative js-hea
0c00: der-wrapper ">.      <a href="#start-of-content" class="px-2 py-
0c40: 4 color-bg-accent-emphasis color-fg-on-emphasis show-on-focus js
0c80: -skip-to-content">Skip to content</a>.      <span data-view-comp
0cc0: onent="true" class="progress-pjax-loader Progress position-fixed
0d00:  width-full">.    <span style="width: 0%;" data-view-component="
0d40: true" class="Progress-item progress-pjax-loader-bar left-0 top-0
0d80:  color-bg-accent-emphasis"></span>.</span>      .      .  ..<scr
0dc0: ipt crossorigin="anonymous" defer="defer" type="application/java
0e00: script" src="https://github.githubassets.com/assets/react-lib-1f
0e40: bfc5be2c18.js"></script>.<script crossorigin="anonymous" defer="
0e80: defer" type="application/javascript" src="https://github.githuba
0ec0: ssets.com/assets/vendors-node_modules_primer_octicons-react_dist
0f00: _index_esm_js-node_modules_primer_react_lib-es-2e8e7c-a58d7c11e8
0f40: 58.js"></script>.<script crossorigin="anonymous" defer="defer" t
0f80: ype="application/javascript" src="https://github.githubassets.co
0fc0: m/assets/vendors-node_modules_primer_react_lib-esm_Box_Box_js-8f
1000: 8c5e2a2cbf.js"></script>.<script crossorigin="anonymous" defer="
1040: defer" type="application/javascript" src="https://github.githuba
1080: ssets.com/assets/vendors-node_modules_primer_react_lib-esm_Butto
10c0: n_Button_js-d5726d25c548.js"></script>.<script crossorigin="anon
1100: ymous" defer="defer" type="application/javascript" src="https://
1140: github.githubassets.com/assets/vendors-node_modules_primer_react
1180: _lib-esm_ActionList_index_js-1501d3ef83c2.js"></script>.<script 
11c0: crossorigin="anonymous" defer="defer" type="application/javascri
1200: pt" src="https://github.githubassets.com/assets/vendors-node_mod
1240: ules_primer_react_lib-esm_Button_IconButton_js-node_modules_prim
1280: er_react_lib--23bcad-01764c79fa41.js"></script>.<script crossori
12c0: gin="anonymous" defer="defer" type="application/javascript" src=
1300: "https://github.githubassets.com/assets/ui_packages_react-core_c
1340: reate-browser-history_ts-ui_packages_react-core_AppContextProvid
1380: er_ts-809ab9-4a2cf4ad7f60.js"></script>.<script crossorigin="ano
13c0: nymous" defer="defer" type="application/javascript" src="https:/
1400: /github.githubassets.com/assets/keyboard-shortcuts-dialog-20a011
1440: 926f27.js"></script>..<react-partial.  partial-name="keyboard-sh
1480: ortcuts-dialog".  data-ssr="false".>.  .  <script type="applicat
14c0: ion/json" data-target="react-partial.embeddedData">{"props":{}}<
1500: /script>.  <div data-target="react-partial.reactRoot"></div>.</r
1540: eact-partial>....      ..        ..            .<script crossori
1580: gin="anonymous" defer="defer" type="application/javascript" src=
15c0: "https://github.githubassets.com/assets/vendors-node_modules_git
1600: hub_remote-form_dist_index_js-node_modules_delegated-events_dist
1640: _inde-94fd67-99519581d0f8.js"></script>.<script crossorigin="ano
1680: nymous" defer="defer" type="application/javascript" src="https:/
16c0: /github.githubassets.com/assets/sessions-694c8423e347.js"></scri
1700: pt>.<header class="Header-old header-logged-out js-details-conta
1740: iner Details position-relative f4 py-3" role="banner" data-color
1780: -mode=light data-light-theme=light data-dark-theme=dark>.  <butt
17c0: on type="button" class="Header-backdrop d-lg-none border-0 posit
1800: ion-fixed top-0 left-0 width-full height-full js-details-target"
1840:  aria-label="Toggle navigation">.    <span class="d-none">Toggle
1880:  navigation</span>.  </button>..  <div class=" d-flex flex-colum
18c0: n flex-lg-row flex-items-center p-responsive height-full positio
1900: n-relative z-1">.    <div class="d-flex flex-justify-between fle
1940: x-items-center width-full width-lg-auto">.      <a class="mr-lg-
1980: 3 color-fg-inherit flex-order-2" href="https://github.com/" aria
19c0: -label="Homepage" data-ga-click="(Logged out) Header, go to home
1a00: page, icon:logo-wordmark">.        <svg height="32" aria-hidden=
1a40: "true" viewBox="0 0 16 16" version="1.1" width="32" data-view-co
1a80: mponent="true" class="octicon octicon-mark-github">.    <path d=
1ac0: "M8 0c4.42 0 8 3.58 8 8a8.013 8.013 0 0 1-5.45 7.59c-.4.08-.55-.
1b00: 17-.55-.38 0-.27.01-1.13.01-2.2 0-.75-.25-1.23-.54-1.48 1.78-.2 
1b40: 3.65-.88 3.65-3.95 0-.88-.31-1.59-.82-2.15.08-.2.36-1.02-.08-2.1
1b80: 2 0 0-.67-.22-2.2.82-.64-.18-1.32-.27-2-.27-.68 0-1.36.09-2 .27-
1bc0: 1.53-1.03-2.2-.82-2.2-.82-.44 1.1-.16 1.92-.08 2.12-.51.56-.82 1
1c00: .28-.82 2.15 0 3.06 1.86 3.75 3.64 3.95-.23.2-.44.55-.51 1.07-.4
1c40: 6.21-1.61.55-2.33-.66-.15-.24-.6-.83-1.23-.82-.67.01-.27.38.01.5
1c80: 3.34.19.73.9.82 1.13.16.45.68 1.31 2.69.94 0 .67.01 1.3.01 1.49 
1cc0: 0 .21-.15.45-.55.38A7.995 7.995 0 0 1 0 8c0-4.42 3.58-8 8-8Z"></
1d00: path>.</svg>.      </a>..      <div class="flex-1">.        <a h
1d40: ref="/login".          class="d-inline-block d-lg-none flex-orde
1d80: r-1 f5 no-underline border color-border-default rounded-2 px-2 p
1dc0: y-1 color-fg-inherit".          data-hydro-click="{&quot;event_t
1e00: ype&quot;:&quot;authentication.click&quot;,&quot;payload&quot;:{
1e40: &quot;location_in_page&quot;:&quot;site header menu&quot;,&quot;
1e80: repository_id&quot;:null,&quot;auth_type&quot;:&quot;SIGN_UP&quo
1ec0: t;,&quot;originating_url&quot;:&quot;https://github.com/&quot;,&
1f00: quot;user_id&quot;:null}}" data-hydro-click-hmac="1ac0bd316eb4ec
1f40: ff0fd1f338bc397cea8b5025ce78fffb7ade6ffdd600360286".          da
1f80: ta-ga-click="(Logged out) Header, clicked Sign in, text:sign-in"
1fc0: >.          Sign in.        </a>.      </div>..      <div class=
2000: "flex-1 flex-order-2 text-right">.        <button aria-label="To
2040: ggle navigation" aria-expanded="false" type="button" data-view-c
2080: omponent="true" class="js-details-target Button--link Button--me
20c0: dium Button d-lg-none color-fg-inherit
20e8: 46F4
20ee:  p-1">  <span class="Button-content">.    <span class="Button-la
212e: bel"><div class="HeaderMenu-toggle-bar rounded my-1"></div>.    
216e:         <div class="HeaderMenu-toggle-bar rounded my-1"></div>. 
21ae:            <div class="HeaderMenu-toggle-bar rounded my-1"></div
21ee: ></span>.  </span>.</button>.      </div>.    </div>...    <div 
222e: class="HeaderMenu--logged-out p-responsive height-fit position-l
226e: g-relative d-lg-flex flex-column flex-auto pt-7 pb-4 top-0">.   
22ae:    <div class="header-menu-wrapper d-flex flex-column flex-self-
22ee: end flex-lg-row flex-justify-between flex-auto p-3 p-lg-0 rounde
232e: d rounded-lg-0 mt-3 mt-lg-0">.          <nav class="mt-0 px-3 px
236e: -lg-0 mb-3 mb-lg-0" aria-label="Global">.            <ul class="
23ae: d-lg-flex list-style-none">.                <li class="HeaderMen
23ee: u-item position-relative flex-wrap flex-justify-between flex-ite
242e: ms-center d-block d-lg-flex flex-lg-nowrap flex-lg-items-center 
246e: js-details-container js-header-menu-item">.      <button type="b
24ae: utton" class="HeaderMenu-link border-0 width-full width-lg-auto 
24ee: px-0 px-lg-2 py-3 py-lg-2 no-wrap d-flex flex-items-center flex-
252e: justify-between js-details-target" aria-expanded="false">.      
256e:   Product.        <svg opacity="0.5" aria-hidden="true" height="
25ae: 16" viewBox="0 0 16 16" version="1.1" width="16" data-view-compo
25ee: nent="true" class="octicon octicon-chevron-down HeaderMenu-icon 
262e: ml-1">.    <path d="M12.78 5.22a.749.749 0 0 1 0 1.06l-4.25 4.25
266e: a.749.749 0 0 1-1.06 0L3.22 6.28a.749.749 0 1 1 1.06-1.06L8 8.93
26ae: 9l3.72-3.719a.749.749 0 0 1 1.06 0Z"></path>.</svg>.      </butt
26ee: on>.      <div class="HeaderMenu-dropdown dropdown-menu rounded 
272e: m-0 p-0 py-2 py-lg-4 position-relative position-lg-absolute left
276e: -0 left-lg-n3 d-lg-flex dropdown-menu-wide">.          <div clas
27ae: s="px-lg-4 border-lg-right mb-4 mb-lg-0 pr-lg-7">.            <u
27ee: l class="list-style-none f5" >.                <li>.  <a class="
282e: HeaderMenu-dropdown-link lh-condensed d-block no-underline posit
286e: ion-relative py-2 Link--secondary d-flex flex-items-center pb-lg
28ae: -3" data-analytics-event="{&quot;category&quot;:&quot;Header dro
28ee: pdown (logged out), Product&quot;,&quot;action&quot;:&quot;click
292e:  to go to Actions&quot;,&quot;label&quot;:&quot;ref_cta:Actions;
296e: &quot;}" href="/features/actions">.      <svg aria-hidden="true"
29ae:  height="24" viewBox="0 0 24 24" version="1.1" width="24" data-v
29ee: iew-component="true" class="octicon octicon-workflow color-fg-su
2a2e: btle mr-3">.    <path d="M1 3a2 2 0 0 1 2-2h6.5a2 2 0 0 1 2 2v6.
2a6e: 5a2 2 0 0 1-2 2H7v4.063C7 16.355 7.644 17 8.438 17H12.5v-2.5a2 2
2aae:  0 0 1 2-2H21a2 2 0 0 1 2 2V21a2 2 0 0 1-2 2h-6.5a2 2 0 0 1-2-2v
2aee: -2.5H8.437A2.939 2.939 0 0 1 5.5 15.562V11.5H3a2 2 0 0 1-2-2Zm2-
2b2e: .5a.5.5 0 0 0-.5.5v6.5a.5.5 0 0 0 .5.5h6.5a.5.5 0 0 0 .5-.5V3a.5
2b6e: .5 0 0 0-.5-.5ZM14.5 14a.5.5 0 0 0-.5.5V21a.5.5 0 0 0 .5.5H21a.5
2bae: .5 0 0 0 .5-.5v-6.5a.5.5 0 0 0-.5-.5Z"></path>.</svg>.      <div
2bee: >.        <div class="color-fg-default h4">Actions</div>.       
2c2e:  Automate any workflow.      </div>..    .</a></li>..           
2c6e:      <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-bl
2cae: ock no-underline position-relative py-2 Link--secondary d-flex f
2cee: lex-items-center pb-lg-3" data-analytics-event="{&quot;category&
2d2e: quot;:&quot;Header dropdown (logged out), Product&quot;,&quot;ac
2d6e: tion&quot;:&quot;click to go to Packages&quot;,&quot;label&quot;
2dae: :&quot;ref_cta:Packages;&quot;}" href="/features/packages">.    
2dee:   <svg aria-hidden="true" height="24" viewBox="0 0 24 24" versio
2e2e: n="1.1" width="24" data-view-component="true" class="octicon oct
2e6e: icon-package color-fg-subtle mr-3">.    <path d="M12.876.64V.639
2eae: l8.25 4.763c.541.313.875.89.875 1.515v9.525a1.75 1.75 0 0 1-.875
2eee:  1.516l-8.25 4.762a1.748 1.748 0 0 1-1.75 0l-8.25-4.763a1.75 1.7
2f2e: 5 0 0 1-.875-1.515V6.917c0-.625.334-1.202.875-1.515L11.126.64a1.
2f6e: 748 1.748 0 0 1 1.75 0Zm-1 1.298L4.251 6.34l7.75 4.474 7.75-4.47
2fae: 4-7.625-4.402a.248.248 0 0 0-.25 0Zm.875 19.123 7.625-4.402a.25.
2fee: 25 0 0 0 .125-.216V7.639l-7.75 4.474ZM3.501 7.64v8.803c0 .09.048
302e: .172.125.216l7.625 4.402v-8.947Z"></path>.</svg>.      <div>.   
306e:      <div class="color-fg-default h4">Packages</div>.        Hos
30ae: t and manage packages.      </div>..    .</a></li>..            
30ee:     <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-blo
312e: ck no-underline position-relative py-2 Link--secondary d-flex fl
316e: ex-items-center pb-lg-3" data-analytics-event="{&quot;category&q
31ae: uot;:&quot;Header dropdown (logged out), Product&quot;,&quot;act
31ee: ion&quot;:&quot;click to go to Security&quot;,&quot;label&quot;:
322e: &quot;ref_cta:Security;&quot;}" href="/features/security">.     
326e:  <svg aria-hidden="true" height="24" viewBox="0 0 24 24" version
32ae: ="1.1" width="24" data-view-component="true" class="octicon octi
32ee: con-shield-check color-fg-subtle mr-3">.    <path d="M16.53 9.78
332e: a.75.75 0 0 0-1.06-1.06L11 13.19l-1.97-1.97a.75.75 0 0 0-1.06 1.
336e: 06l2.5 2.5a.75.75 0 0 0 1.06 0l5-5Z"></path><path d="m12.54.637 
33ae: 8.25 2.675A1.75 1.75 0 0 1 22 4.976V10c0 6.19-3.771 10.704-9.401
33ee:  12.83a1.704 1.704 0 0 1-1.198 0C5.77 20.705 2 16.19 2 10V4.976c
342e: 0-.758.489-1.43 1.21-1.664L11.46.637a1.748 1.748 0 0 1 1.08 0Zm-
346e: .617 1.426-8.25 2.676a.249.249 0 0 0-.173.237V10c0 5.46 3.28 9.4
34ae: 83 8.43 11.426a.199.199 0 0 0 .14 0C17.22 19.483 20.5 15.461 20.
34ee: 5 10V4.976a.25.25 0 0 0-.173-.237l-8.25-2.676a.253.253 0 0 0-.15
352e: 4 0Z"></path>.</svg>.      <div>.        <div class="color-fg-de
356e: fault h4">Security</div>.        Find and fix vulnerabilities.  
35ae:     </div>..    .</a></li>..                <li>.  <a class="Hea
35ee: derMenu-dropdown-link lh-condensed d-block no-underline position
362e: -relative py-2 Link--secondary d-flex flex-items-center pb-lg-3"
366e:  data-analytics-event="{&quot;category&quot;:&quot;Header dropdo
36ae: wn (logged out), Product&quot;,&quot;action&quot;:&quot;click to
36ee:  go to Codespaces&quot;,&quot;label&quot;:&quot;ref_cta:Codespac
372e: es;&quot;}" href="/features/codespaces">.      <svg aria-hidden=
376e: "true" height="24" viewBox="0 0 24 24" version="1.1" width="24" 
37ae: data-view-component="true" class="octicon octicon-codespaces col
37ee: or-fg-subtle mr-3">.    <path d="M3.5 3.75C3.5 2.784 4.284 2 5.2
382e: 5 2h13.5c.966 0 1.75.784 1.75 1.75v7.5A1.75 1.75 0 0 1 18.75 13H
386e: 5.25a1.75 1.75 0 0 1-1.75-1.75Zm-2 12c0-.966.784-1.75 1.75-1.75h
38ae: 17.5c.966 0 1.75.784 1.75 1.75v4a1.75 1.75 0 0 1-1.75 1.75H3.25a
38ee: 1.75 1.75 0 0 1-1.75-1.75ZM5.25 3.5a.25.25 0 0 0-.25.25v7.5c0 .1
392e: 38.112.25.25.25h13.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-
396e: .25Zm-2 12a.25.25 0 0 0-.25.25v4c0 .138.112.25.25.25h17.5a.25.25
39ae:  0 0 0 .25-.25v-4a.25.25 0 0 0-.25-.25Z"></path><path d="M10 17.
39ee: 75a.75.75 0 0 1 .75-.75h6.5a.75.75 0 0 1 0 1.5h-6.5a.75.75 0 0 1
3a2e: -.75-.75Zm-4 0a.75.75 0 0 1 .75-.75h.5a.75.75 0 0 1 0 1.5h-.5a.7
3a6e: 5.75 0 0 1-.75-.75Z"></path>.</svg>.      <div>.        <div cla
3aae: ss="color-fg-default h4">Codespaces</div>.        Instant dev en
3aee: vironments.      </div>..    .</a></li>..                <li>.  
3b2e: <a class="HeaderMenu-dropdown-link lh-condensed d-block no-under
3b6e: line position-relative py-2 Link--secondary d-flex flex-item
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 5480 bytes (0x1568)
0000: s-center pb-lg-3" data-analytics-event="{&quot;category&quot;:&q
0040: uot;Header dropdown (logged out), Product&quot;,&quot;action&quo
0080: t;:&quot;click to go to Copilot&quot;,&quot;label&quot;:&quot;re
00c0: f_cta:Copilot;&quot;}" href="/features/copilot">.      <svg aria
0100: -hidden="true" height="24" viewBox="0 0 24 24" version="1.1" wid
0140: th="24" data-view-component="true" class="octicon octicon-copilo
0180: t color-fg-subtle mr-3">.    <path d="M23.922 16.992c-.861 1.495
01c0: -5.859 5.023-11.922 5.023-6.063 0-11.061-3.528-11.922-5.023A.641
0200: .641 0 0 1 0 16.736v-2.869a.841.841 0 0 1 .053-.22c.372-.935 1.3
0240: 47-2.292 2.605-2.656.167-.429.414-1.055.644-1.517a10.195 10.195 
0280: 0 0 1-.052-1.086c0-1.331.282-2.499 1.132-3.368.397-.406.89-.717 
02c0: 1.474-.952 1.399-1.136 3.392-2.093 6.122-2.093 2.731 0 4.767.957
0300:  6.166 2.093.584.235 1.077.546 1.474.952.85.869 1.132 2.037 1.13
0340: 2 3.368 0 .368-.014.733-.052 1.086.23.462.477 1.088.644 1.517 1.
0380: 258.364 2.233 1.721 2.605 2.656a.832.832 0 0 1 .053.22v2.869a.64
03c0: 1.641 0 0 1-.078.256ZM12.172 11h-.344a4.323 4.323 0 0 1-.355.508
0400: C10.703 12.455 9.555 13 7.965 13c-1.725 0-2.989-.359-3.782-1.259
0440: a2.005 2.005 0 0 1-.085-.104L4 11.741v6.585c1.435.779 4.514 2.17
0480: 9 8 2.179 3.486 0 6.565-1.4 8-2.179v-6.585l-.098-.104s-.033.045-
04c0: .085.104c-.793.9-2.057 1.259-3.782 1.259-1.59 0-2.738-.545-3.508
0500: -1.492a4.323 4.323 0 0 1-.355-.508h-.016.016Zm.641-2.935c.136 1.
0540: 057.403 1.913.878 2.497.442.544 1.134.938 2.344.938 1.573 0 2.29
0580: 2-.337 2.657-.751.384-.435.558-1.15.558-2.361 0-1.14-.243-1.847-
05c0: .705-2.319-.477-.488-1.319-.862-2.824-1.025-1.487-.161-2.192.138
0600: -2.533.529-.269.307-.437.808-.438 1.578v.021c0 .265.021.562.063.
0640: 893Zm-1.626 0c.042-.331.063-.628.063-.894v-.02c-.001-.77-.169-1.
0680: 271-.438-1.578-.341-.391-1.046-.69-2.533-.529-1.505.163-2.347.53
06c0: 7-2.824 1.025-.462.472-.705 1.179-.705 2.319 0 1.211.175 1.926.5
0700: 58 2.361.365.414 1.084.751 2.657.751 1.21 0 1.902-.394 2.344-.93
0740: 8.475-.584.742-1.44.878-2.497Z"></path><path d="M14.5 14.25a1 1 
0780: 0 0 1 1 1v2a1 1 0 0 1-2 0v-2a1 1 0 0 1 1-1Zm-5 0a1 1 0 0 1 1 1v2
07c0: a1 1 0 0 1-2 0v-2a1 1 0 0 1 1-1Z"></path>.</svg>.      <div>.   
0800:      <div class="color-fg-default h4">Copilot</div>.        Writ
0840: e better code with AI.      </div>..    .</a></li>..            
0880:     <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-blo
08c0: ck no-underline position-relative py-2 Link--secondary d-flex fl
0900: ex-items-center pb-lg-3" data-analytics-event="{&quot;category&q
0940: uot;:&quot;Header dropdown (logged out), Product&quot;,&quot;act
0980: ion&quot;:&quot;click to go to Code review&quot;,&quot;label&quo
09c0: t;:&quot;ref_cta:Code review;&quot;}" href="/features/code-revie
0a00: w">.      <svg aria-hidden="true" height="24" viewBox="0 0 24 24
0a40: " version="1.1" width="24" data-view-component="true" class="oct
0a80: icon octicon-code-review color-fg-subtle mr-3">.    <path d="M10
0ac0: .3 6.74a.75.75 0 0 1-.04 1.06l-2.908 2.7 2.908 2.7a.75.75 0 1 1-
0b00: 1.02 1.1l-3.5-3.25a.75.75 0 0 1 0-1.1l3.5-3.25a.75.75 0 0 1 1.06
0b40: .04Zm3.44 1.06a.75.75 0 1 1 1.02-1.1l3.5 3.25a.75.75 0 0 1 0 1.1
0b80: l-3.5 3.25a.75.75 0 1 1-1.02-1.1l2.908-2.7-2.908-2.7Z"></path><p
0bc0: ath d="M1.5 4.25c0-.966.784-1.75 1.75-1.75h17.5c.966 0 1.75.784 
0c00: 1.75 1.75v12.5a1.75 1.75 0 0 1-1.75 1.75h-9.69l-3.573 3.573A1.45
0c40: 8 1.458 0 0 1 5 21.043V18.5H3.25a1.75 1.75 0 0 1-1.75-1.75ZM3.25
0c80:  4a.25.25 0 0 0-.25.25v12.5c0 .138.112.25.25.25h2.5a.75.75 0 0 1
0cc0:  .75.75v3.19l3.72-3.72a.749.749 0 0 1 .53-.22h10a.25.25 0 0 0 .2
0d00: 5-.25V4.25a.25.25 0 0 0-.25-.25Z"></path>.</svg>.      <div>.   
0d40:      <div class="color-fg-default h4">Code review</div>.        
0d80: Manage code changes.      </div>..    .</a></li>..              
0dc0:   <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-block
0e00:  no-underline position-relative py-2 Link--secondary d-flex flex
0e40: -items-center pb-lg-3" data-analytics-event="{&quot;category&quo
0e80: t;:&quot;Header dropdown (logged out), Product&quot;,&quot;actio
0ec0: n&quot;:&quot;click to go to Issues&quot;,&quot;label&quot;:&quo
0f00: t;ref_cta:Issues;&quot;}" href="/features/issues">.      <svg ar
0f40: ia-hidden="true" height="24" viewBox="0 0 24 24" version="1.1" w
0f80: idth="24" data-view-component="true" class="octicon octicon-issu
0fc0: e-opened color-fg-subtle mr-3">.    <path d="M12 1c6.075 0 11 4.
1000: 925 11 11s-4.925 11-11 11S1 18.075 1 12 5.925 1 12 1ZM2.5 12a9.5
1040:  9.5 0 0 0 9.5 9.5 9.5 9.5 0 0 0 9.5-9.5A9.5 9.5 0 0 0 12 2.5 9.
1080: 5 9.5 0 0 0 2.5 12Zm9.5 2a2 2 0 1 1-.001-3.999A2 2 0 0 1 12 14Z"
10c0: ></path>.</svg>.      <div>.        <div class="color-fg-default
1100:  h4">Issues</div>.        Plan and track work.      </div>..    
1140: .</a></li>..                <li>.  <a class="HeaderMenu-dropdown
1180: -link lh-condensed d-block no-underline position-relative py-2 L
11c0: ink--secondary d-flex flex-items-center" data-analytics-event="{
1200: &quot;category&quot;:&quot;Header dropdown (logged out), Product
1240: &quot;,&quot;action&quot;:&quot;click to go to Discussions&quot;
1280: ,&quot;label&quot;:&quot;ref_cta:Discussions;&quot;}" href="/fea
12c0: tures/discussions">.      <svg aria-hidden="true" height="24" vi
1300: ewBox="0 0 24 24" version="1.1" width="24" data-view-component="
1340: true" class="octicon octicon-comment-discussion color-fg-subtle 
1380: mr-3">.    <path d="M1.75 1h12.5c.966 0 1.75.784 1.75 1.75v9.5A1
13c0: .75 1.75 0 0 1 14.25 14H8.061l-2.574 2.573A1.458 1.458 0 0 1 3 1
1400: 5.543V14H1.75A1.75 1.75 0 0 1 0 12.25v-9.5C0 1.784.784 1 1.75 1Z
1440: M1.5 2.75v9.5c0 .138.112.25.25.25h2a.75.75 0 0 1 .75.75v2.19l2.7
1480: 2-2.72a.749.749 0 0 1 .53-.22h6.5a.25.25 0 0 0 .25-.25v-9.5a.25.
14c0: 25 0 0 0-.25-.25H1.75a.25.25 0 0 0-.25.25Z"></path><path d="M22.
1500: 5 8.75a.25.25 0 0 0-.25-.25h-3.5a.75.75 0 0 1 0-1.5h3.5c.966 0 1
1540: .75.784 1.75 1.75v9.5A1.75 1.75 0 0 1 22
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 9952 bytes (0x26e0)
0000: .25 20H21v1.543a1.457 1.457 0 0 1-2.487 1.03L15.939 20H10.75A1.7
0040: 5 1.75 0 0 1 9 18.25v-1.465a.75.75 0 0 1 1.5 0v1.465c0 .138.112.
0080: 25.25.25h5.5a.75.75 0 0 1 .53.22l2.72 2.72v-2.19a.75.75 0 0 1 .7
00c0: 5-.75h2a.25.25 0 0 0 .25-.25v-9.5Z"></path>.</svg>.      <div>. 
0100:        <div class="color-fg-default h4">Discussions</div>.      
0140:   Collaborate outside of code.      </div>..    .</a></li>..    
0180:         </ul>.          </div>.          <div class="px-lg-4">. 
01c0:              <span class="d-block h4 color-fg-default my-1" id="
0200: product-explore-heading">Explore</span>.            <ul class="l
0240: ist-style-none f5" aria-labelledby="product-explore-heading">.  
0280:               <li>.  <a class="HeaderMenu-dropdown-link lh-conde
02c0: nsed d-block no-underline position-relative py-2 Link--secondary
0300: " data-analytics-event="{&quot;category&quot;:&quot;Header dropd
0340: own (logged out), Product&quot;,&quot;action&quot;:&quot;click t
0380: o go to All features&quot;,&quot;label&quot;:&quot;ref_cta:All f
03c0: eatures;&quot;}" href="/features">.      All features..    .</a>
0400: </li>..                <li>.  <a class="HeaderMenu-dropdown-link
0440:  lh-condensed d-block no-underline position-relative py-2 Link--
0480: secondary" target="_blank" data-analytics-event="{&quot;category
04c0: &quot;:&quot;Header dropdown (logged out), Product&quot;,&quot;a
0500: ction&quot;:&quot;click to go to Documentation&quot;,&quot;label
0540: &quot;:&quot;ref_cta:Documentation;&quot;}" href="https://docs.g
0580: ithub.com">.      Documentation..    <svg aria-hidden="true" hei
05c0: ght="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-
0600: component="true" class="octicon octicon-link-external HeaderMenu
0640: -external-icon color-fg-subtle">.    <path d="M3.75 2h3.5a.75.75
0680:  0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.25.25h8.
06c0: 5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.5A1.75 1.75 0 0
0700:  1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2.784 2.784 2 3.
0740: 75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.25.25 0 0 1-.427.
0780: 177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.018.751.751 0 0 1
07c0: -.018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 10.604 1Z"></path
0800: >.</svg>.</a></li>..                <li>.  <a class="HeaderMenu-
0840: dropdown-link lh-condensed d-block no-underline position-relativ
0880: e py-2 Link--secondary" target="_blank" data-analytics-event="{&
08c0: quot;category&quot;:&quot;Header dropdown (logged out), Product&
0900: quot;,&quot;action&quot;:&quot;click to go to GitHub Skills&quot
0940: ;,&quot;label&quot;:&quot;ref_cta:GitHub Skills;&quot;}" href="h
0980: ttps://skills.github.com/">.      GitHub Skills..    <svg aria-h
09c0: idden="true" height="16" viewBox="0 0 16 16" version="1.1" width
0a00: ="16" data-view-component="true" class="octicon octicon-link-ext
0a40: ernal HeaderMenu-external-icon color-fg-subtle">.    <path d="M3
0a80: .75 2h3.5a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138
0ac0: .112.25.25.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3
0b00: .5A1.75 1.75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 
0b40: 2.784 2.784 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.2
0b80: 5.25 0 0 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.0
0bc0: 18.751.751 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 1
0c00: 0.604 1Z"></path>.</svg>.</a></li>..                <li>.  <a cl
0c40: ass="HeaderMenu-dropdown-link lh-condensed d-block no-underline 
0c80: position-relative py-2 Link--secondary" target="_blank" data-ana
0cc0: lytics-event="{&quot;category&quot;:&quot;Header dropdown (logge
0d00: d out), Product&quot;,&quot;action&quot;:&quot;click to go to Bl
0d40: og&quot;,&quot;label&quot;:&quot;ref_cta:Blog;&quot;}" href="htt
0d80: ps://github.blog">.      Blog..    <svg aria-hidden="true" heigh
0dc0: t="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-co
0e00: mponent="true" class="octicon octicon-link-external HeaderMenu-e
0e40: xternal-icon color-fg-subtle">.    <path d="M3.75 2h3.5a.75.75 0
0e80:  0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.25.25h8.5a
0ec0: .25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.5A1.75 1.75 0 0 1
0f00:  12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2.784 2.784 2 3.75
0f40:  2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.25.25 0 0 1-.427.17
0f80: 7L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.
0fc0: 018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 10.604 1Z"></path>.
1000: </svg>.</a></li>..            </ul>.          </div>.      </div
1040: >.</li>...                <li class="HeaderMenu-item position-re
1080: lative flex-wrap flex-justify-between flex-items-center d-block 
10c0: d-lg-flex flex-lg-nowrap flex-lg-items-center js-details-contain
1100: er js-header-menu-item">.      <button type="button" class="Head
1140: erMenu-link border-0 width-full width-lg-auto px-0 px-lg-2 py-3 
1180: py-lg-2 no-wrap d-flex flex-items-center flex-justify-between js
11c0: -details-target" aria-expanded="false">.        Solutions.      
1200:   <svg opacity="0.5" aria-hidden="true" height="16" viewBox="0 0
1240:  16 16" version="1.1" width="16" data-view-component="true" clas
1280: s="octicon octicon-chevron-down HeaderMenu-icon ml-1">.    <path
12c0:  d="M12.78 5.22a.749.749 0 0 1 0 1.06l-4.25 4.25a.749.749 0 0 1-
1300: 1.06 0L3.22 6.28a.749.749 0 1 1 1.06-1.06L8 8.939l3.72-3.719a.74
1340: 9.749 0 0 1 1.06 0Z"></path>.</svg>.      </button>.      <div c
1380: lass="HeaderMenu-dropdown dropdown-menu rounded m-0 p-0 py-2 py-
13c0: lg-4 position-relative position-lg-absolute left-0 left-lg-n3 px
1400: -lg-4">.          <div class="border-bottom pb-3 mb-3">.        
1440:       <span class="d-block h4 color-fg-default my-1" id="solutio
1480: ns-for-heading">For</span>.            <ul class="list-style-non
14c0: e f5" aria-labelledby="solutions-for-heading">.                <
1500: li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-block no
1540: -underline position-relative py-2 Link--secondary" data-analytic
1580: s-event="{&quot;category&quot;:&quot;Header dropdown (logged out
15c0: ), Solutions&quot;,&quot;action&quot;:&quot;click to go to Enter
1600: prise&quot;,&quot;label&quot;:&quot;ref_cta:Enterprise;&quot;}" 
1640: href="/enterprise">.      Enterprise..    .</a></li>..          
1680:       <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-b
16c0: lock no-underlin
16d2: 263A
16d8: e position-relative py-2 Link--secondary" data-analytics-event="
1718: {&quot;category&quot;:&quot;Header dropdown (logged out), Soluti
1758: ons&quot;,&quot;action&quot;:&quot;click to go to Teams&quot;,&q
1798: uot;label&quot;:&quot;ref_cta:Teams;&quot;}" href="/team">.     
17d8:  Teams..    .</a></li>..                <li>.  <a class="HeaderM
1818: enu-dropdown-link lh-condensed d-block no-underline position-rel
1858: ative py-2 Link--secondary" data-analytics-event="{&quot;categor
1898: y&quot;:&quot;Header dropdown (logged out), Solutions&quot;,&quo
18d8: t;action&quot;:&quot;click to go to Startups&quot;,&quot;label&q
1918: uot;:&quot;ref_cta:Startups;&quot;}" href="/enterprise/startups"
1958: >.      Startups..    .</a></li>..                <li>.  <a clas
1998: s="HeaderMenu-dropdown-link lh-condensed d-block no-underline po
19d8: sition-relative py-2 Link--secondary" target="_blank" data-analy
1a18: tics-event="{&quot;category&quot;:&quot;Header dropdown (logged 
1a58: out), Solutions&quot;,&quot;action&quot;:&quot;click to go to Ed
1a98: ucation&quot;,&quot;label&quot;:&quot;ref_cta:Education;&quot;}"
1ad8:  href="https://education.github.com">.      Education..    <svg 
1b18: aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
1b58:  width="16" data-view-component="true" class="octicon octicon-li
1b98: nk-external HeaderMenu-external-icon color-fg-subtle">.    <path
1bd8:  d="M3.75 2h3.5a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c
1c18: 0 .138.112.25.25.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1
1c58: .5 0v3.5A1.75 1.75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-
1c98: 8.5C2 2.784 2.784 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.
1cd8: 146a.25.25 0 0 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.
1d18: 042-.018.751.751 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.25 0
1d58:  0 1 10.604 1Z"></path>.</svg>.</a></li>..            </ul>.    
1d98:       </div>.          <div class="border-bottom pb-3 mb-3">.   
1dd8:            <span class="d-block h4 color-fg-default my-1" id="so
1e18: lutions-by-solution-heading">By Solution</span>.            <ul 
1e58: class="list-style-none f5" aria-labelledby="solutions-by-solutio
1e98: n-heading">.                <li>.  <a class="HeaderMenu-dropdown
1ed8: -link lh-condensed d-block no-underline position-relative py-2 L
1f18: ink--secondary" data-analytics-event="{&quot;category&quot;:&quo
1f58: t;Header dropdown (logged out), Solutions&quot;,&quot;action&quo
1f98: t;:&quot;click to go to CI/CD &amp;amp; Automation&quot;,&quot;l
1fd8: abel&quot;:&quot;ref_cta:CI/CD &amp;amp; Automation;&quot;}" hre
2018: f="/solutions/ci-cd/">.      CI/CD &amp; Automation..    .</a></
2058: li>..                <li>.  <a class="HeaderMenu-dropdown-link l
2098: h-condensed d-block no-underline position-relative py-2 Link--se
20d8: condary" data-analytics-event="{&quot;category&quot;:&quot;Heade
2118: r dropdown (logged out), Solutions&quot;,&quot;action&quot;:&quo
2158: t;click to go to DevOps&quot;,&quot;label&quot;:&quot;ref_cta:De
2198: vOps;&quot;}" href="/solutions/devops/">.      DevOps..    .</a>
21d8: </li>..                <li>.  <a class="HeaderMenu-dropdown-link
2218:  lh-condensed d-block no-underline position-relative py-2 Link--
2258: secondary" target="_blank" data-analytics-event="{&quot;category
2298: &quot;:&quot;Header dropdown (logged out), Solutions&quot;,&quot
22d8: ;action&quot;:&quot;click to go to DevSecOps&quot;,&quot;label&q
2318: uot;:&quot;ref_cta:DevSecOps;&quot;}" href="https://resources.gi
2358: thub.com/devops/fundamentals/devsecops/">.      DevSecOps..    <
2398: svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="
23d8: 1.1" width="16" data-view-component="true" class="octicon octico
2418: n-link-external HeaderMenu-external-icon color-fg-subtle">.    <
2458: path d="M3.75 2h3.5a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v
2498: 8.5c0 .138.112.25.25.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0
24d8:  1 1.5 0v3.5A1.75 1.75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.
2518: 25v-8.5C2 2.784 2.784 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.2
2558: 5v4.146a.25.25 0 0 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 
2598: 1-1.042-.018.751.751 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.
25d8: 25 0 0 1 10.604 1Z"></path>.</svg>.</a></li>..            </ul>.
2618:           </div>.          <div class="">.              <span cl
2658: ass="d-block h4 color-fg-default my-1" id="solutions-resources-h
2698: eading">Resources</span>.            <ul class="list-style-none 
26d8: f5" aria
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 15366 bytes (0x3c06)
0000: -labelledby="solutions-resources-heading">.                <li>.
0040:   <a class="HeaderMenu-dropdown-link lh-condensed d-block no-und
0080: erline position-relative py-2 Link--secondary" target="_blank" d
00c0: ata-analytics-event="{&quot;category&quot;:&quot;Header dropdown
0100:  (logged out), Solutions&quot;,&quot;action&quot;:&quot;click to
0140:  go to Learning Pathways&quot;,&quot;label&quot;:&quot;ref_cta:L
0180: earning Pathways;&quot;}" href="https://resources.github.com/lea
01c0: rn/pathways/">.      Learning Pathways..    <svg aria-hidden="tr
0200: ue" height="16" viewBox="0 0 16 16" version="1.1" width="16" dat
0240: a-view-component="true" class="octicon octicon-link-external Hea
0280: derMenu-external-icon color-fg-subtle">.    <path d="M3.75 2h3.5
02c0: a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.2
0300: 5.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.5A1.75 1
0340: .75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2.784 2.7
0380: 84 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.25.25 0 0 
03c0: 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.018.751.75
0400: 1 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 10.604 1Z"
0440: ></path>.</svg>.</a></li>..                <li>.  <a class="Head
0480: erMenu-dropdown-link lh-condensed d-block no-underline position-
04c0: relative py-2 Link--secondary" target="_blank" data-analytics-ev
0500: ent="{&quot;category&quot;:&quot;Header dropdown (logged out), S
0540: olutions&quot;,&quot;action&quot;:&quot;click to go to White pap
0580: ers, Ebooks, Webinars&quot;,&quot;label&quot;:&quot;ref_cta:Whit
05c0: e papers, Ebooks, Webinars;&quot;}" href="https://resources.gith
0600: ub.com/">.      White papers, Ebooks, Webinars..    <svg aria-hi
0640: dden="true" height="16" viewBox="0 0 16 16" version="1.1" width=
0680: "16" data-view-component="true" class="octicon octicon-link-exte
06c0: rnal HeaderMenu-external-icon color-fg-subtle">.    <path d="M3.
0700: 75 2h3.5a.75.75 0 0 1 0 1.5h-3.5a.25.25 0 0 0-.25.25v8.5c0 .138.
0740: 112.25.25.25h8.5a.25.25 0 0 0 .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.
0780: 5A1.75 1.75 0 0 1 12.25 14h-8.5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2
07c0: .784 2.784 2 3.75 2Zm6.854-1h4.146a.25.25 0 0 1 .25.25v4.146a.25
0800: .25 0 0 1-.427.177L13.03 4.03 9.28 7.78a.751.751 0 0 1-1.042-.01
0840: 8.751.751 0 0 1-.018-1.042l3.75-3.75-1.543-1.543A.25.25 0 0 1 10
0880: .604 1Z"></path>.</svg>.</a></li>..                <li>.  <a cla
08c0: ss="HeaderMenu-dropdown-link lh-condensed d-block no-underline p
0900: osition-relative py-2 Link--secondary" data-analytics-event="{&q
0940: uot;category&quot;:&quot;Header dropdown (logged out), Solutions
0980: &quot;,&quot;action&quot;:&quot;click to go to Customer Stories&
09c0: quot;,&quot;label&quot;:&quot;ref_cta:Customer Stories;&quot;}" 
0a00: href="/customer-stories">.      Customer Stories..    .</a></li>
0a40: ..                <li>.  <a class="HeaderMenu-dropdown-link lh-c
0a80: ondensed d-block no-underline position-relative py-2 Link--secon
0ac0: dary" target="_blank" data-analytics-event="{&quot;category&quot
0b00: ;:&quot;Header dropdown (logged out), Solutions&quot;,&quot;acti
0b40: on&quot;:&quot;click to go to Partners&quot;,&quot;label&quot;:&
0b80: quot;ref_cta:Partners;&quot;}" href="https://partner.github.com/
0bc0: ">.      Partners..    <svg aria-hidden="true" height="16" viewB
0c00: ox="0 0 16 16" version="1.1" width="16" data-view-component="tru
0c40: e" class="octicon octicon-link-external HeaderMenu-external-icon
0c80:  color-fg-subtle">.    <path d="M3.75 2h3.5a.75.75 0 0 1 0 1.5h-
0cc0: 3.5a.25.25 0 0 0-.25.25v8.5c0 .138.112.25.25.25h8.5a.25.25 0 0 0
0d00:  .25-.25v-3.5a.75.75 0 0 1 1.5 0v3.5A1.75 1.75 0 0 1 12.25 14h-8
0d40: .5A1.75 1.75 0 0 1 2 12.25v-8.5C2 2.784 2.784 2 3.75 2Zm6.854-1h
0d80: 4.146a.25.25 0 0 1 .25.25v4.146a.25.25 0 0 1-.427.177L13.03 4.03
0dc0:  9.28 7.78a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042l3.
0e00: 75-3.75-1.543-1.543A.25.25 0 0 1 10.604 1Z"></path>.</svg>.</a><
0e40: /li>..            </ul>.          </div>.      </div>.</li>...  
0e80:               <li class="HeaderMenu-item position-relative flex-
0ec0: wrap flex-justify-between flex-items-center d-block d-lg-flex fl
0f00: ex-lg-nowrap flex-lg-items-center js-details-container js-header
0f40: -menu-item">.      <button type="button" class="HeaderMenu-link 
0f80: border-0 width-full width-lg-auto px-0 px-lg-2 py-3 py-lg-2 no-w
0fc0: rap d-flex flex-items-center flex-justify-between js-details-tar
1000: get" aria-expanded="false">.        Open Source.        <svg opa
1040: city="0.5" aria-hidden="true" height="16" viewBox="0 0 16 16" ve
1080: rsion="1.1" width="16" data-view-component="true" class="octicon
10c0:  octicon-chevron-down HeaderMenu-icon ml-1">.    <path d="M12.78
1100:  5.22a.749.749 0 0 1 0 1.06l-4.25 4.25a.749.749 0 0 1-1.06 0L3.2
1140: 2 6.28a.749.749 0 1 1 1.06-1.06L8 8.939l3.72-3.719a.749.749 0 0 
1180: 1 1.06 0Z"></path>.</svg>.      </button>.      <div class="Head
11c0: erMenu-dropdown dropdown-menu rounded m-0 p-0 py-2 py-lg-4 posit
1200: ion-relative position-lg-absolute left-0 left-lg-n3 px-lg-4">.  
1240:         <div class="border-bottom pb-3 mb-3">.            <ul cl
1280: ass="list-style-none f5" >.                <li>.  <a class="Head
12c0: erMenu-dropdown-link lh-condensed d-block no-underline position-
1300: relative py-2 Link--secondary d-flex flex-items-center" data-ana
1340: lytics-event="{&quot;category&quot;:&quot;Header dropdown (logge
1380: d out), Open Source&quot;,&quot;action&quot;:&quot;click to go t
13c0: o GitHub Sponsors&quot;,&quot;label&quot;:&quot;ref_cta:GitHub S
1400: ponsors;&quot;}" href="/sponsors">.      .      <div>.        <d
1440: iv class="color-fg-default h4">GitHub Sponsors</div>.        Fun
1480: d open source developers.      </div>..    .</a></li>..         
14c0:    </ul>.          </div>.          <div class="border-bottom pb
1500: -3 mb-3">.            <ul class="list-style-none f5" >.         
1540:        <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-
1580: block no-underline position-relative py-2 Link--secondary d-flex
15c0:  flex-items-center" data-analytics-event="{&quot;category&quot;:
1600: &quot;Header dropdown (logged out), Open Source&qu
1634: 1062
163a: ot;,&quot;action&quot;:&quot;click to go to The ReadME Project&q
167a: uot;,&quot;label&quot;:&quot;ref_cta:The ReadME Project;&quot;}"
16ba:  href="/readme">.      .      <div>.        <div class="color-fg
16fa: -default h4">The ReadME Project</div>.        GitHub community a
173a: rticles.      </div>..    .</a></li>..            </ul>.        
177a:   </div>.          <div class="">.              <span class="d-b
17ba: lock h4 color-fg-default my-1" id="open-source-repositories-head
17fa: ing">Repositories</span>.            <ul class="list-style-none 
183a: f5" aria-labelledby="open-source-repositories-heading">.        
187a:         <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d
18ba: -block no-underline position-relative py-2 Link--secondary" data
18fa: -analytics-event="{&quot;category&quot;:&quot;Header dropdown (l
193a: ogged out), Open Source&quot;,&quot;action&quot;:&quot;click to 
197a: go to Topics&quot;,&quot;label&quot;:&quot;ref_cta:Topics;&quot;
19ba: }" href="/topics">.      Topics..    .</a></li>..               
19fa:  <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-block 
1a3a: no-underline position-relative py-2 Link--secondary" data-analyt
1a7a: ics-event="{&quot;category&quot;:&quot;Header dropdown (logged o
1aba: ut), Open Source&quot;,&quot;action&quot;:&quot;click to go to T
1afa: rending&quot;,&quot;label&quot;:&quot;ref_cta:Trending;&quot;}" 
1b3a: href="/trending">.      Trending..    .</a></li>..              
1b7a:   <li>.  <a class="HeaderMenu-dropdown-link lh-condensed d-block
1bba:  no-underline position-relative py-2 Link--secondary" data-analy
1bfa: tics-event="{&quot;category&quot;:&quot;Header dropdown (logged 
1c3a: out), Open Source&quot;,&quot;action&quot;:&quot;click to go to 
1c7a: Collections&quot;,&quot;label&quot;:&quot;ref_cta:Collections;&q
1cba: uot;}" href="/collections">.      Collections..    .</a></li>.. 
1cfa:            </ul>.          </div>.      </div>.</li>...         
1d3a:        <li class="HeaderMenu-item position-relative flex-wrap fl
1d7a: ex-justify-between flex-items-center d-block d-lg-flex flex-lg-n
1dba: owrap flex-lg-items-center js-details-container js-header-menu-i
1dfa: tem">.    <a class="HeaderMenu-link no-underline px-0 px-lg-2 py
1e3a: -3 py-lg-2 d-block d-lg-inline-block" data-analytics-event="{&qu
1e7a: ot;category&quot;:&quot;Header menu top item (logged out)&quot;,
1eba: &quot;action&quot;:&quot;click to go to Pricing&quot;,&quot;labe
1efa: l&quot;:&quot;ref_cta:Pricing;&quot;}" href="/pricing">Pricing</
1f3a: a>.</li>..            </ul>.          </nav>..        <div class
1f7a: ="d-lg-flex flex-items-center mb-3 mb-lg-0 text-center text-lg-l
1fba: eft ml-3" style="">.                ...<qbsearch-input class="se
1ffa: arch-input" data-scope="" data-custom-scopes-path="/search/custo
203a: m_scopes" data-delete-custom-scopes-csrf="A4Yk_jkZSBnIfdbwYfC-3z
207a: Ao1qFHz-tZoZ-1x_BmBH09VGkCZJzErZs9lbvCHuWh9q8aLfB893JnzHQmof3J8g
20ba: " data-max-custom-scopes="10" data-header-redesign-enabled="fals
20fa: e" data-initial-value="" data-blackbird-suggestions-path="/searc
213a: h/suggestions" data-jump-to-suggestions-path="/_graphql/GetSugge
217a: stedNavigationDestinations" data-current-repository="" data-curr
21ba: ent-org="" data-current-owner="" data-logged-in="false" data-cop
21fa: ilot-chat-enabled="false" data-blackbird-indexed-repo-csrf="<esi
223a: :include src=&quot;/_esi/rails_csrf_token_form_hidden?r=MPuy3xnD
227a: a0BqL6L0iH90CHGiJRtvw45FGtu8sZu3%2BjBAe1uRbE2egKXiVfiwydO4M4sm40
22ba: svufzG%2F9p4ZkeY0yzbJ1xMXCmYVd0ikE8HCC3T5mQxq6uMRyoyvxgf58faOCPz
22fa: %2FZOZrI4Mz%2Bb6gScJ9f9bkM648c%2Ba1k8qseKM0vJ0l6rjE1AaMCM0lpL3We
233a: 5XyAyPXzKm4zE9cOCy7c%2FGQOm8oly1ExmuVvZoY5PIqug7OFUfnDGxCj5fMPiQ
237a: zg8rChLE0mfu%2FVPqN5wtDE9o44vxBALQ7D2Z5YaGOUuGHWy1a%2BotAM6hDsmn
23ba: xnadjAypHZCZXZ39uM4sJE%2Bo%2B7mNF9p%2BnpK9YyE%2F8jShsKkD3bboMnu0
23fa: j%2BZFTDZ1zAH6lKN%2FIUfVtzfRlFzkTTkbnP9r%2F%2BTEOGdtfQoCWoCZwx2I
243a: h%2B4DYulzgIs6znQQn7NnQY6xx3RCeArXfwLWJ2rNnkQsxj6Oo1%2F1fUmRjSAU
247a: 5FUJUepwqPRPjTg%3D--2LUJjF0lQ9mwQvS%2B--L66vtwNMXVhySu%2BdnEOZaQ
24ba: %3D%3D&quot; />">.  <div.    class="search-input-container searc
24fa: h-with-dialog position-relative d-flex flex-row flex-items-cente
253a: r mr-4 rounded".    data-action="click:qbsearch-input#searchInpu
257a: tContainerClicked".  >.      <button.        type="button".     
25ba:    class="header-search-button placeholder  input-button form-co
25fa: ntrol d-flex flex-1 flex-self-stretch flex-items-center no-wrap 
263a: width-full py-0 pl-2 pr-0 text-left border-0 box-shadow-none".  
267a:       data-target="qbsearch-input.
269e: 25A2
26a4: inputButton".        placeholder="Search or jump to...".        
26e4: data-hotkey=s,/.        autocapitalize="off".        data-action
2724: ="click:qbsearch-input#handleExpand".      >.        <div class=
2764: "mr-2 color-fg-muted">.          <svg aria-hidden="true" height=
27a4: "16" viewBox="0 0 16 16" version="1.1" width="16" data-view-comp
27e4: onent="true" class="octicon octicon-search">.    <path d="M10.68
2824:  11.74a6 6 0 0 1-7.922-8.982 6 6 0 0 1 8.982 7.922l3.04 3.04a.74
2864: 9.749 0 0 1-.326 1.275.749.749 0 0 1-.734-.215ZM11.5 7a4.499 4.4
28a4: 99 0 1 0-8.997 0A4.499 4.499 0 0 0 11.5 7Z"></path>.</svg>.     
28e4:    </div>.        <span class="flex-1" data-target="qbsearch-inp
2924: ut.inputButtonText">Search or jump to...</span>.          <div c
2964: lass="d-flex" data-target="qbsearch-input.hotkeyIndicator">.    
29a4:         <svg xmlns="http://www.w3.org/2000/svg" width="22" heigh
29e4: t="20" aria-hidden="true" class="mr-1"><path fill="none" stroke=
2a24: "#979A9C" opacity=".4" d="M3.5.5h12c1.7 0 3 1.3 3 3v13c0 1.7-1.3
2a64:  3-3 3h-12c-1.7 0-3-1.3-3-3v-13c0-1.7 1.3-3 3-3z"></path><path f
2aa4: ill="#979A9C" d="M11.8 6L8 15.1h-.9L10.8 6h1z"></path></svg>..  
2ae4:         </div>.      </button>..    <input type="hidden" name="t
2b24: ype" class="js-site-search-type-field">..    .<div class="Overla
2b64: y--hidden " data-modal-dialog-overlay>.  <modal-dialog data-acti
2ba4: on="close:qbsearch-input#handleClose cancel:qbsearch-input#handl
2be4: eClose" data-target="qbsearch-input.searchSuggestionsDialog" rol
2c24: e="dialog" id="search-suggestions-dialog" aria-modal="true" aria
2c64: -labelledby="search-suggestions-dialog-header" data-view-compone
2ca4: nt="true" class="Overlay Overlay--width-large Overlay--height-au
2ce4: to">.      <h1 id="search-suggestions-dialog-header" class="sr-o
2d24: nly">Search code, repositories, users, issues, pull requests...<
2d64: /h1>.    <div class="Overlay-body Overlay-body--paddingNone">.  
2da4:     .          <div data-view-component="true">        <div clas
2de4: s="search-suggestions position-fixed width-full color-shadow-lar
2e24: ge border color-fg-default color-bg-default overflow-hidden d-fl
2e64: ex flex-column query-builder-container".          style="border-
2ea4: radius: 12px;".          data-target="qbsearch-input.queryBuilde
2ee4: rContainer".          hidden.        >.          <!-- '"` --><!-
2f24: - </textarea></xmp> --></option></form><form id="query-builder-t
2f64: est-form" action="" accept-charset="UTF-8" method="get">.  <quer
2fa4: y-builder data-target="qbsearch-input.queryBuilder" id="query-bu
2fe4: ilder-query-builder-test" data-filter-key=":" data-view-componen
3024: t="true" class="QueryBuilder search-query-builder">.    <div cla
3064: ss="FormControl FormControl--fullWidth">.      <label id="query-
30a4: builder-test-label" for="query-builder-test" class="FormControl-
30e4: label sr-only">.        Search.      </label>.      <div.       
3124:  class="QueryBuilder-StyledInput width-fit ".        data-target
3164: ="query-builder.styledInput".      >.          <span id="query-b
31a4: uilder-test-leadingvisual-wrap" class="FormControl-input-leading
31e4: VisualWrap QueryBuilder-leadingVisualWrap">.            <svg ari
3224: a-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" wi
3264: dth="16" data-view-component="true" class="octicon octicon-searc
32a4: h FormControl-input-leadingVisual">.    <path d="M10.68 11.74a6 
32e4: 6 0 0 1-7.922-8.982 6 6 0 0 1 8.982 7.922l3.04 3.04a.749.749 0 0
3324:  1-.326 1.275.749.749 0 0 1-.734-.215ZM11.5 7a4.499 4.499 0 1 0-
3364: 8.997 0A4.499 4.499 0 0 0 11.5 7Z"></path>.</svg>.          </sp
33a4: an>.        <div data-target="query-builder.styledInputContainer
33e4: " class="QueryBuilder-StyledInputContainer">.          <div.    
3424:         aria-hidden="true".            class="QueryBuilder-Style
3464: dInputContent".            data-target="query-builder.styledInpu
34a4: tContent".          ></div>.          <div class="QueryBuilder-I
34e4: nputWrapper">.            <div aria-hidden="true" class="QueryBu
3524: ilder-Sizer" data-target="query-builder.sizer"></div>.          
3564:   <input id="query-builder-test" name="query-builder-test" value
35a4: ="" autocomplete="off" type="text" role="combobox" spellcheck="f
35e4: alse" aria-expanded="false" aria-describedby="validation-5ebbc67
3624: c-7307-4f5b-9fb1-6a4f2bc4d822" data-target="query-builder.input"
3664:  data-action=".          input:query-builder#inputChange.       
36a4:    blur:query-builder#inputBlur.          keydown:query-builder#
36e4: inputKeydown.          focus:query-builder#inputFocus.        " 
3724: data-view-component="true" class="FormControl-input QueryBuilder
3764: -Input FormControl-medium" />.          </div>.        </div>.  
37a4:         <span class="sr-only" id="query-builder-test-clear">Clea
37e4: r</span>.          <button role="button" id="query-builder-test-
3824: clear-button" aria-labelledby="query-builder-test-clear query-bu
3864: ilder-test-label" data-target="query-builder.clearButton" data-a
38a4: ction=".                click:query-builder#clear.              
38e4:   focus:query-builder#clearButtonFocus.                blur:quer
3924: y-builder#clearButtonBlur.              " variant="small" hidden
3964: ="hidden" type="button" data-view-component="true" class="Button
39a4:  Button--iconOnly Button--invisible Button--medium mr-1 px-2 py-
39e4: 0 d-flex flex-items-center rounded-1 color-fg-muted">  <svg aria
3a24: -hidden="true" height="16" viewBox="0 0 16 16" version="1.1" wid
3a64: th="16" data-view-component="true" class="octicon octicon-x-circ
3aa4: le-fill Button-visual">.    <path d="M2.343 13.657A8 8 0 1 1 13.
3ae4: 658 2.343 8 8 0 0 1 2.343 13.657ZM6.03 4.97a.751.751 0 0 0-1.042
3b24: .018.751.751 0 0 0-.018 1.042L6.94 8 4.97 9.97a.749.749 0 0 0 .3
3b64: 26 1.275.749.749 0 0 0 .734-.215L8 9.06l1.97 1.97a.749.749 0 0 0
3ba4:  1.275-.326.749.749 0 0 0-.215-.734L9.06 8l1.97-1.97a.749.749 0 
3be4: 0 0-.326-1.275.749.749 0 0 0-.734.
== Info: schannel: failed to decrypt data, need more data
<= Recv data, 30192 bytes (0x75f0)
0000: 215L8 6.94Z"></path>.</svg>.</button>..      </div>.      <templ
0040: ate id="search-icon">.  <svg aria-hidden="true" height="16" view
0080: Box="0 0 16 16" version="1.1" width="16" data-view-component="tr
00c0: ue" class="octicon octicon-search">.    <path d="M10.68 11.74a6 
0100: 6 0 0 1-7.922-8.982 6 6 0 0 1 8.982 7.922l3.04 3.04a.749.749 0 0
0140:  1-.326 1.275.749.749 0 0 1-.734-.215ZM11.5 7a4.499 4.499 0 1 0-
0180: 8.997 0A4.499 4.499 0 0 0 11.5 7Z"></path>.</svg>.</template>..<
01c0: template id="code-icon">.  <svg aria-hidden="true" height="16" v
0200: iewBox="0 0 16 16" version="1.1" width="16" data-view-component=
0240: "true" class="octicon octicon-code">.    <path d="m11.28 3.22 4.
0280: 25 4.25a.75.75 0 0 1 0 1.06l-4.25 4.25a.749.749 0 0 1-1.275-.326
02c0: .749.749 0 0 1 .215-.734L13.94 8l-3.72-3.72a.749.749 0 0 1 .326-
0300: 1.275.749.749 0 0 1 .734.215Zm-6.56 0a.751.751 0 0 1 1.042.018.7
0340: 51.751 0 0 1 .018 1.042L2.06 8l3.72 3.72a.749.749 0 0 1-.326 1.2
0380: 75.749.749 0 0 1-.734-.215L.47 8.53a.75.75 0 0 1 0-1.06Z"></path
03c0: >.</svg>.</template>..<template id="file-code-icon">.  <svg aria
0400: -hidden="true" height="16" viewBox="0 0 16 16" version="1.1" wid
0440: th="16" data-view-component="true" class="octicon octicon-file-c
0480: ode">.    <path d="M4 1.75C4 .784 4.784 0 5.75 0h5.586c.464 0 .9
04c0: 09.184 1.237.513l2.914 2.914c.329.328.513.773.513 1.237v8.586A1.
0500: 75 1.75 0 0 1 14.25 15h-9a.75.75 0 0 1 0-1.5h9a.25.25 0 0 0 .25-
0540: .25V6h-2.75A1.75 1.75 0 0 1 10 4.25V1.5H5.75a.25.25 0 0 0-.25.25
0580: v2.5a.75.75 0 0 1-1.5 0Zm1.72 4.97a.75.75 0 0 1 1.06 0l2 2a.75.7
05c0: 5 0 0 1 0 1.06l-2 2a.749.749 0 0 1-1.275-.326.749.749 0 0 1 .215
0600: -.734l1.47-1.47-1.47-1.47a.75.75 0 0 1 0-1.06ZM3.28 7.78 1.81 9.
0640: 25l1.47 1.47a.751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018l-
0680: 2-2a.75.75 0 0 1 0-1.06l2-2a.751.751 0 0 1 1.042.018.751.751 0 0
06c0:  1 .018 1.042Zm8.22-6.218V4.25c0 .138.112.25.25.25h2.688l-.011-.
0700: 013-2.914-2.914-.013-.011Z"></path>.</svg>.</template>..<templat
0740: e id="history-icon">.  <svg aria-hidden="true" height="16" viewB
0780: ox="0 0 16 16" version="1.1" width="16" data-view-component="tru
07c0: e" class="octicon octicon-history">.    <path d="m.427 1.927 1.2
0800: 15 1.215a8.002 8.002 0 1 1-1.6 5.685.75.75 0 1 1 1.493-.154 6.5 
0840: 6.5 0 1 0 1.18-4.458l1.358 1.358A.25.25 0 0 1 3.896 6H.25A.25.25
0880:  0 0 1 0 5.75V2.104a.25.25 0 0 1 .427-.177ZM7.75 4a.75.75 0 0 1 
08c0: .75.75v2.992l2.028.812a.75.75 0 0 1-.557 1.392l-2.5-1A.751.751 0
0900:  0 1 7 8.25v-3.5A.75.75 0 0 1 7.75 4Z"></path>.</svg>.</template
0940: >..<template id="repo-icon">.  <svg aria-hidden="true" height="1
0980: 6" viewBox="0 0 16 16" version="1.1" width="16" data-view-compon
09c0: ent="true" class="octicon octicon-repo">.    <path d="M2 2.5A2.5
0a00:  2.5 0 0 1 4.5 0h8.75a.75.75 0 0 1 .75.75v12.5a.75.75 0 0 1-.75.
0a40: 75h-2.5a.75.75 0 0 1 0-1.5h1.75v-2h-8a1 1 0 0 0-.714 1.7.75.75 0
0a80:  1 1-1.072 1.05A2.495 2.495 0 0 1 2 11.5Zm10.5-1h-8a1 1 0 0 0-1 
0ac0: 1v6.708A2.486 2.486 0 0 1 4.5 9h8ZM5 12.25a.25.25 0 0 1 .25-.25h
0b00: 3.5a.25.25 0 0 1 .25.25v3.25a.25.25 0 0 1-.4.2l-1.45-1.087a.249.
0b40: 249 0 0 0-.3 0L5.4 15.7a.25.25 0 0 1-.4-.2Z"></path>.</svg>.</te
0b80: mplate>..<template id="bookmark-icon">.  <svg aria-hidden="true"
0bc0:  height="16" viewBox="0 0 16 16" version="1.1" width="16" data-v
0c00: iew-component="true" class="octicon octicon-bookmark">.    <path
0c40:  d="M3 2.75C3 1.784 3.784 1 4.75 1h6.5c.966 0 1.75.784 1.75 1.75
0c80: v11.5a.75.75 0 0 1-1.227.579L8 11.722l-3.773 3.107A.751.751 0 0 
0cc0: 1 3 14.25Zm1.75-.25a.25.25 0 0 0-.25.25v9.91l3.023-2.489a.75.75 
0d00: 0 0 1 .954 0l3.023 2.49V2.75a.25.25 0 0 0-.25-.25Z"></path>.</sv
0d40: g>.</template>..<template id="plus-circle-icon">.  <svg aria-hid
0d80: den="true" height="16" viewBox="0 0 16 16" version="1.1" width="
0dc0: 16" data-view-component="true" class="octicon octicon-plus-circl
0e00: e">.    <path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0ZM1.5 8a6.5 6.
0e40: 5 0 1 0 13 0 6.5 6.5 0 0 0-13 0Zm7.25-3.25v2.5h2.5a.75.75 0 0 1 
0e80: 0 1.5h-2.5v2.5a.75.75 0 0 1-1.5 0v-2.5h-2.5a.75.75 0 0 1 0-1.5h2
0ec0: .5v-2.5a.75.75 0 0 1 1.5 0Z"></path>.</svg>.</template>..<templa
0f00: te id="circle-icon">.  <svg aria-hidden="true" height="16" viewB
0f40: ox="0 0 16 16" version="1.1" width="16" data-view-component="tru
0f80: e" class="octicon octicon-dot-fill">.    <path d="M8 4a4 4 0 1 1
0fc0:  0 8 4 4 0 0 1 0-8Z"></path>.</svg>.</template>..<template id="t
1000: rash-icon">.  <svg aria-hidden="true" height="16" viewBox="0 0 1
1042: 6D30
1048: 6 16" version="1.1" width="16" data-view-component="true" class=
1088: "octicon octicon-trash">.    <path d="M11 1.75V3h2.25a.75.75 0 0
10c8:  1 0 1.5H2.75a.75.75 0 0 1 0-1.5H5V1.75C5 .784 5.784 0 6.75 0h2.
1108: 5C10.216 0 11 .784 11 1.75ZM4.496 6.675l.66 6.6a.25.25 0 0 0 .24
1148: 9.225h5.19a.25.25 0 0 0 .249-.225l.66-6.6a.75.75 0 0 1 1.492.149
1188: l-.66 6.6A1.748 1.748 0 0 1 10.595 15h-5.19a1.75 1.75 0 0 1-1.74
11c8: 1-1.575l-.66-6.6a.75.75 0 1 1 1.492-.15ZM6.5 1.75V3h3V1.75a.25.2
1208: 5 0 0 0-.25-.25h-2.5a.25.25 0 0 0-.25.25Z"></path>.</svg>.</temp
1248: late>..<template id="team-icon">.  <svg aria-hidden="true" heigh
1288: t="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-co
12c8: mponent="true" class="octicon octicon-people">.    <path d="M2 5
1308: .5a3.5 3.5 0 1 1 5.898 2.549 5.508 5.508 0 0 1 3.034 4.084.75.75
1348:  0 1 1-1.482.235 4 4 0 0 0-7.9 0 .75.75 0 0 1-1.482-.236A5.507 5
1388: .507 0 0 1 3.102 8.05 3.493 3.493 0 0 1 2 5.5ZM11 4a3.001 3.001 
13c8: 0 0 1 2.22 5.018 5.01 5.01 0 0 1 2.56 3.012.749.749 0 0 1-.885.9
1408: 54.752.752 0 0 1-.549-.514 3.507 3.507 0 0 0-2.522-2.372.75.75 0
1448:  0 1-.574-.73v-.352a.75.75 0 0 1 .416-.672A1.5 1.5 0 0 0 11 5.5.
1488: 75.75 0 0 1 11 4Zm-5.5-.5a2 2 0 1 0-.001 3.999A2 2 0 0 0 5.5 3.5
14c8: Z"></path>.</svg>.</template>..<template id="project-icon">.  <s
1508: vg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1
1548: .1" width="16" data-view-component="true" class="octicon octicon
1588: -project">.    <path d="M1.75 0h12.5C15.216 0 16 .784 16 1.75v12
15c8: .5A1.75 1.75 0 0 1 14.25 16H1.75A1.75 1.75 0 0 1 0 14.25V1.75C0 
1608: .784.784 0 1.75 0ZM1.5 1.75v12.5c0 .138.112.25.25.25h12.5a.25.25
1648:  0 0 0 .25-.25V1.75a.25.25 0 0 0-.25-.25H1.75a.25.25 0 0 0-.25.2
1688: 5ZM11.75 3a.75.75 0 0 1 .75.75v7.5a.75.75 0 0 1-1.5 0v-7.5a.75.7
16c8: 5 0 0 1 .75-.75Zm-8.25.75a.75.75 0 0 1 1.5 0v5.5a.75.75 0 0 1-1.
1708: 5 0ZM8 3a.75.75 0 0 1 .75.75v3.5a.75.75 0 0 1-1.5 0v-3.5A.75.75 
1748: 0 0 1 8 3Z"></path>.</svg>.</template>..<template id="pencil-ico
1788: n">.  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" ve
17c8: rsion="1.1" width="16" data-view-component="true" class="octicon
1808:  octicon-pencil">.    <path d="M11.013 1.427a1.75 1.75 0 0 1 2.4
1848: 74 0l1.086 1.086a1.75 1.75 0 0 1 0 2.474l-8.61 8.61c-.21.21-.47.
1888: 364-.756.445l-3.251.93a.75.75 0 0 1-.927-.928l.929-3.25c.081-.28
18c8: 6.235-.547.445-.758l8.61-8.61Zm.176 4.823L9.75 4.81l-6.286 6.287
1908: a.253.253 0 0 0-.064.108l-.558 1.953 1.953-.558a.253.253 0 0 0 .
1948: 108-.064Zm1.238-3.763a.25.25 0 0 0-.354 0L10.811 3.75l1.439 1.44
1988:  1.263-1.263a.25.25 0 0 0 0-.354Z"></path>.</svg>.</template>..<
19c8: template id="copilot-icon">.  <svg aria-hidden="true" height="16
1a08: " viewBox="0 0 16 16" version="1.1" width="16" data-view-compone
1a48: nt="true" class="octicon octicon-copilot">.    <path d="M7.998 1
1a88: 5.035c-4.562 0-7.873-2.914-7.998-3.749V9.338c.085-.628.677-1.686
1ac8:  1.588-2.065.013-.07.024-.143.036-.218.029-.183.06-.384.126-.612
1b08: -.201-.508-.254-1.084-.254-1.656 0-.87.128-1.769.693-2.484.579-.
1b48: 733 1.494-1.124 2.724-1.261 1.206-.134 2.262.034 2.944.765.05.05
1b88: 3.096.108.139.165.044-.057.094-.112.143-.165.682-.731 1.738-.899
1bc8:  2.944-.765 1.23.137 2.145.528 2.724 1.261.566.715.693 1.614.693
1c08:  2.484 0 .572-.053 1.148-.254 1.656.066.228.098.429.126.612.012.
1c48: 076.024.148.037.218.924.385 1.522 1.471 1.591 2.095v1.872c0 .766
1c88: -3.351 3.795-8.002 3.795Zm0-1.485c2.28 0 4.584-1.11 5.002-1.433V
1cc8: 7.862l-.023-.116c-.49.21-1.075.291-1.727.291-1.146 0-2.059-.327-
1d08: 2.71-.991A3.222 3.222 0 0 1 8 6.303a3.24 3.24 0 0 1-.544.743c-.6
1d48: 5.664-1.563.991-2.71.991-.652 0-1.236-.081-1.727-.291l-.023.116v
1d88: 4.255c.419.323 2.722 1.433 5.002 1.433ZM6.762 2.83c-.193-.206-.6
1dc8: 37-.413-1.682-.297-1.019.113-1.479.404-1.713.7-.247.312-.369.789
1e08: -.369 1.554 0 .793.129 1.171.308 1.371.162.181.519.379 1.442.379
1e48: .853 0 1.339-.235 1.638-.54.315-.322.527-.827.617-1.553.117-.935
1e88: -.037-1.395-.241-1.614Zm4.155-.297c-1.044-.116-1.488.091-1.681.2
1ec8: 97-.204.219-.359.679-.242 1.614.091.726.303 1.231.618 1.553.299.
1f08: 305.784.54 1.638.54.922 0 1.28-.198 1.442-.379.179-.2.308-.578.3
1f48: 08-1.371 0-.765-.123-1.242-.37-1.554-.233-.296-.693-.587-1.713-.
1f88: 7Z"></path><path d="M6.25 9.037a.75.75 0 0 1 .75.75v1.501a.75.75
1fc8:  0 0 1-1.5 0V9.787a.75.75 0 0 1 .75-.75Zm4.25.75v1.501a.75.75 0 
2008: 0 1-1.5 0V9.787a.75.75 0 0 1 1.5 0Z"></path>.</svg>.</template>.
2048: .<template id="workflow-icon">.  <svg aria-hidden="true" height=
2088: "16" viewBox="0 0 16 16" version="1.1" width="16" data-view-comp
20c8: onent="true" class="octicon octicon-workflow">.    <path d="M0 1
2108: .75C0 .784.784 0 1.75 0h3.5C6.216 0 7 .784 7 1.75v3.5A1.75 1.75 
2148: 0 0 1 5.25 7H4v4a1 1 0 0 0 1 1h4v-1.25C9 9.784 9.784 9 10.75 9h3
2188: .5c.966 0 1.75.784 1.75 1.75v3.5A1.75 1.75 0 0 1 14.25 16h-3.5A1
21c8: .75 1.75 0 0 1 9 14.25v-.75H5A2.5 2.5 0 0 1 2.5 11V7h-.75A1.75 1
2208: .75 0 0 1 0 5.25Zm1.75-.25a.25.25 0 0 0-.25.25v3.5c0 .138.112.25
2248: .25.25h3.5a.25.25 0 0 0 .25-.25v-3.5a.25.25 0 0 0-.25-.25Zm9 9a.
2288: 25.25 0 0 0-.25.25v3.5c0 .138.112.25.25.25h3.5a.25.25 0 0 0 .25-
22c8: .25v-3.5a.25.25 0 0 0-.25-.25Z"></path>.</svg>.</template>..<tem
2308: plate id="book-icon">.  <svg aria-hidden="true" height="16" view
2348: Box="0 0 16 16" version="1.1" width="16" data-view-component="tr
2388: ue" class="octicon octicon-book">.    <path d="M0 1.75A.75.75 0 
23c8: 0 1 .75 1h4.253c1.227 0 2.317.59 3 1.501A3.743 3.743 0 0 1 11.00
2408: 6 1h4.245a.75.75 0 0 1 .75.75v10.5a.75.75 0 0 1-.75.75h-4.507a2.
2448: 25 2.25 0 0 0-1.591.659l-.622.621a.75.75 0 0 1-1.06 0l-.622-.621
2488: A2.25 2.25 0 0 0 5.258 13H.75a.75.75 0 0 1-.75-.75Zm7.251 10.324
24c8: .004-5.073-.002-2.253A2.25 2.25 0 0 0 5.003 2.5H1.5v9h3.757a3.75
2508:  3.75 0 0 1 1.994.574ZM8.755 4.75l-.004 7.322a3.752 3.752 0 0 1 
2548: 1.992-.572H14.5v-9h-3.495a2.25 2.25 0 0 0-2.25 2.25Z"></path>.</
2588: svg>.</template>..<template id="code-review-icon">.  <svg aria-h
25c8: idden="true" height="16" viewBox="0 0 16 16" version="1.1" width
2608: ="16" data-view-component="true" class="octicon octicon-code-rev
2648: iew">.    <path d="M1.75 1h12.5c.966 0 1.75.784 1.75 1.75v8.5A1.
2688: 75 1.75 0 0 1 14.25 13H8.061l-2.574 2.573A1.458 1.458 0 0 1 3 14
26c8: .543V13H1.75A1.75 1.75 0 0 1 0 11.25v-8.5C0 1.784.784 1 1.75 1ZM
2708: 1.5 2.75v8.5c0 .138.112.25.25.25h2a.75.75 0 0 1 .75.75v2.19l2.72
2748: -2.72a.749.749 0 0 1 .53-.22h6.5a.25.25 0 0 0 .25-.25v-8.5a.25.2
2788: 5 0 0 0-.25-.25H1.75a.25.25 0 0 0-.25.25Zm5.28 1.72a.75.75 0 0 1
27c8:  0 1.06L5.31 7l1.47 1.47a.751.751 0 0 1-.018 1.042.751.751 0 0 1
2808: -1.042.018l-2-2a.75.75 0 0 1 0-1.06l2-2a.75.75 0 0 1 1.06 0Zm2.4
2848: 4 0a.75.75 0 0 1 1.06 0l2 2a.75.75 0 0 1 0 1.06l-2 2a.751.751 0 
2888: 0 1-1.042-.018.751.751 0 0 1-.018-1.042L10.69 7 9.22 5.53a.75.75
28c8:  0 0 1 0-1.06Z"></path>.</svg>.</template>..<template id="codesp
2908: aces-icon">.  <svg aria-hidden="true" height="16" viewBox="0 0 1
2948: 6 16" version="1.1" width="16" data-view-component="true" class=
2988: "octicon octicon-codespaces">.    <path d="M0 11.25c0-.966.784-1
29c8: .75 1.75-1.75h12.5c.966 0 1.75.784 1.75 1.75v3A1.75 1.75 0 0 1 1
2a08: 4.25 16H1.75A1.75 1.75 0 0 1 0 14.25Zm2-9.5C2 .784 2.784 0 3.75 
2a48: 0h8.5C13.216 0 14 .784 14 1.75v5a1.75 1.75 0 0 1-1.75 1.75h-8.5A
2a88: 1.75 1.75 0 0 1 2 6.75Zm1.75-.25a.25.25 0 0 0-.25.25v5c0 .138.11
2ac8: 2.25.25.25h8.5a.25.25 0 0 0 .25-.25v-5a.25.25 0 0 0-.25-.25Zm-2 
2b08: 9.5a.25.25 0 0 0-.25.25v3c0 .138.112.25.25.25h12.5a.25.25 0 0 0 
2b48: .25-.25v-3a.25.25 0 0 0-.25-.25Z"></path><path d="M7 12.75a.75.7
2b88: 5 0 0 1 .75-.75h4.5a.75.75 0 0 1 0 1.5h-4.5a.75.75 0 0 1-.75-.75
2bc8: Zm-4 0a.75.75 0 0 1 .75-.75h.5a.75.75 0 0 1 0 1.5h-.5a.75.75 0 0
2c08:  1-.75-.75Z"></path>.</svg>.</template>..<template id="comment-i
2c48: con">.  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" 
2c88: version="1.1" width="16" data-view-component="true" class="octic
2cc8: on octicon-comment">.    <path d="M1 2.75C1 1.784 1.784 1 2.75 1
2d08: h10.5c.966 0 1.75.784 1.75 1.75v7.5A1.75 1.75 0 0 1 13.25 12H9.0
2d48: 6l-2.573 2.573A1.458 1.458 0 0 1 4 13.543V12H2.75A1.75 1.75 0 0 
2d88: 1 1 10.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h
2dc8: 2a.75.75 0 0 1 .75.75v2.19l2.72-2.72a.749.749 0 0 1 .53-.22h4.5a
2e08: .25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>.</svg>.
2e48: </template>..<template id="comment-discussion-icon">.  <svg aria
2e88: -hidden="true" height="16" viewBox="0 0 16 16" version="1.1" wid
2ec8: th="16" data-view-component="true" class="octicon octicon-commen
2f08: t-discussion">.    <path d="M1.75 1h8.5c.966 0 1.75.784 1.75 1.7
2f48: 5v5.5A1.75 1.75 0 0 1 10.25 10H7.061l-2.574 2.573A1.458 1.458 0 
2f88: 0 1 2 11.543V10h-.25A1.75 1.75 0 0 1 0 8.25v-5.5C0 1.784.784 1 1
2fc8: .75 1ZM1.5 2.75v5.5c0 .138.112.25.25.25h1a.75.75 0 0 1 .75.75v2.
3008: 19l2.72-2.72a.749.749 0 0 1 .53-.22h3.5a.25.25 0 0 0 .25-.25v-5.
3048: 5a.25.25 0 0 0-.25-.25h-8.5a.25.25 0 0 0-.25.25Zm13 2a.25.25 0 0
3088:  0-.25-.25h-.5a.75.75 0 0 1 0-1.5h.5c.966 0 1.75.784 1.75 1.75v5
30c8: .5A1.75 1.75 0 0 1 14.25 12H14v1.543a1.458 1.458 0 0 1-2.487 1.0
3108: 3L9.22 12.28a.749.749 0 0 1 .326-1.275.749.749 0 0 1 .734.215l2.
3148: 22 2.22v-2.19a.75.75 0 0 1 .75-.75h1a.25.25 0 0 0 .25-.25Z"></pa
3188: th>.</svg>.</template>..<template id="organization-icon">.  <svg
31c8:  aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1
3208: " width="16" data-view-component="true" class="octicon octicon-o
3248: rganization">.    <path d="M1.75 16A1.75 1.75 0 0 1 0 14.25V1.75
3288: C0 .784.784 0 1.75 0h8.5C11.216 0 12 .784 12 1.75v12.5c0 .085-.0
32c8: 06.168-.018.25h2.268a.25.25 0 0 0 .25-.25V8.285a.25.25 0 0 0-.11
3308: 1-.208l-1.055-.703a.749.749 0 1 1 .832-1.248l1.055.703c.487.325.
3348: 779.871.779 1.456v5.965A1.75 1.75 0 0 1 14.25 16h-3.5a.766.766 0
3388:  0 1-.197-.026c-.099.017-.2.026-.303.026h-3a.75.75 0 0 1-.75-.75
33c8: V14h-1v1.25a.75.75 0 0 1-.75.75Zm-.25-1.75c0 .138.112.25.25.25H4
3408: v-1.25a.75.75 0 0 1 .75-.75h2.5a.75.75 0 0 1 .75.75v1.25h2.25a.2
3448: 5.25 0 0 0 .25-.25V1.75a.25.25 0 0 0-.25-.25h-8.5a.25.25 0 0 0-.
3488: 25.25ZM3.75 6h.5a.75.75 0 0 1 0 1.5h-.5a.75.75 0 0 1 0-1.5ZM3 3.
34c8: 75A.75.75 0 0 1 3.75 3h.5a.75.75 0 0 1 0 1.5h-.5A.75.75 0 0 1 3 
3508: 3.75Zm4 3A.75.75 0 0 1 7.75 6h.5a.75.75 0 0 1 0 1.5h-.5A.75.75 0
3548:  0 1 7 6.75ZM7.75 3h.5a.75.75 0 0 1 0 1.5h-.5a.75.75 0 0 1 0-1.5
3588: ZM3 9.75A.75.75 0 0 1 3.75 9h.5a.75.75 0 0 1 0 1.5h-.5A.75.75 0 
35c8: 0 1 3 9.75ZM7.75 9h.5a.75.75 0 0 1 0 1.5h-.5a.75.75 0 0 1 0-1.5Z
3608: "></path>.</svg>.</template>..<template id="rocket-icon">.  <svg
3648:  aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1
3688: " width="16" data-view-component="true" class="octicon octicon-r
36c8: ocket">.    <path d="M14.064 0h.186C15.216 0 16 .784 16 1.75v.18
3708: 6a8.752 8.752 0 0 1-2.564 6.186l-.458.459c-.314.314-.641.616-.97
3748: 9.904v3.207c0 .608-.315 1.172-.833 1.49l-2.774 1.707a.749.749 0 
3788: 0 1-1.11-.418l-.954-3.102a1.214 1.214 0 0 1-.145-.125L3.754 9.81
37c8: 6a1.218 1.218 0 0 1-.124-.145L.528 8.717a.749.749 0 0 1-.418-1.1
3808: 1l1.71-2.774A1.748 1.748 0 0 1 3.31 4h3.204c.288-.338.59-.665.90
3848: 4-.979l.459-.458A8.749 8.749 0 0 1 14.064 0ZM8.938 3.623h-.002l-
3888: .458.458c-.76.76-1.437 1.598-2.02 2.5l-1.5 2.317 2.143 2.143 2.3
38c8: 17-1.5c.902-.583 1.74-1.26 2.499-2.02l.459-.458a7.25 7.25 0 0 0 
3908: 2.123-5.127V1.75a.25.25 0 0 0-.25-.25h-.186a7.249 7.249 0 0 0-5.
3948: 125 2.123ZM3.56 14.56c-.732.732-2.334 1.045-3.005 1.148a.234.234
3988:  0 0 1-.201-.064.234.234 0 0 1-.064-.201c.103-.671.416-2.273 1.1
39c8: 5-3.003a1.502 1.502 0 1 1 2.12 2.12Zm6.94-3.935c-.088.06-.177.11
3a08: 8-.266.175l-2.35 1.521.548 1.783 1.949-1.2a.25.25 0 0 0 .119-.21
3a48: 3ZM3.678 8.116 5.2 5.766c.058-.09.117-.178.176-.266H3.309a.25.25
3a88:  0 0 0-.213.119l-1.2 1.95ZM12 5a1 1 0 1 1-2 0 1 1 0 0 1 2 0Z"></
3ac8: path>.</svg>.</template>..<template id="shield-check-icon">.  <s
3b08: vg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1
3b48: .1" width="16" data-view-component="true" class="octicon octicon
3b88: -shield-check">.    <path d="m8.533.133 5.25 1.68A1.75 1.75 0 0 
3bc8: 1 15 3.48V7c0 1.566-.32 3.182-1.303 4.682-.983 1.498-2.585 2.813
3c08: -5.032 3.855a1.697 1.697 0 0 1-1.33 0c-2.447-1.042-4.049-2.357-5
3c48: .032-3.855C1.32 10.182 1 8.566 1 7V3.48a1.75 1.75 0 0 1 1.217-1.
3c88: 667l5.25-1.68a1.748 1.748 0 0 1 1.066 0Zm-.61 1.429.001.001-5.25
3cc8:  1.68a.251.251 0 0 0-.174.237V7c0 1.36.275 2.666 1.057 3.859.784
3d08:  1.194 2.121 2.342 4.366 3.298a.196.196 0 0 0 .154 0c2.245-.957 
3d48: 3.582-2.103 4.366-3.297C13.225 9.666 13.5 8.358 13.5 7V3.48a.25.
3d88: 25 0 0 0-.174-.238l-5.25-1.68a.25.25 0 0 0-.153 0ZM11.28 6.28l-3
3dc8: .5 3.5a.75.75 0 0 1-1.06 0l-1.5-1.5a.749.749 0 0 1 .326-1.275.74
3e08: 9.749 0 0 1 .734.215l.97.97 2.97-2.97a.751.751 0 0 1 1.042.018.7
3e48: 51.751 0 0 1 .018 1.042Z"></path>.</svg>.</template>..<template 
3e88: id="heart-icon">.  <svg aria-hidden="true" height="16" viewBox="
3ec8: 0 0 16 16" version="1.1" width="16" data-view-component="true" c
3f08: lass="octicon octicon-heart">.    <path d="m8 14.25.345.666a.75.
3f48: 75 0 0 1-.69 0l-.008-.004-.018-.01a7.152 7.152 0 0 1-.31-.17 22.
3f88: 055 22.055 0 0 1-3.434-2.414C2.045 10.731 0 8.35 0 5.5 0 2.836 2
3fc8: .086 1 4.25 1 5.797 1 7.153 1.802 8 3.02 8.847 1.802 10.203 1 11
4008: .75 1 13.914 1 16 2.836 16 5.5c0 2.85-2.045 5.231-3.885 6.818a22
4048: .066 22.066 0 0 1-3.744 2.584l-.018.01-.006.003h-.002ZM4.25 2.5c
4088: -1.336 0-2.75 1.164-2.75 3 0 2.15 1.58 4.144 3.365 5.682A20.58 2
40c8: 0.58 0 0 0 8 13.393a20.58 20.58 0 0 0 3.135-2.211C12.92 9.644 14
4108: .5 7.65 14.5 5.5c0-1.836-1.414-3-2.75-3-1.373 0-2.609.986-3.029 
4148: 2.456a.749.749 0 0 1-1.442 0C6.859 3.486 5.623 2.5 4.25 2.5Z"></
4188: path>.</svg>.</template>..<template id="server-icon">.  <svg ari
41c8: a-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" wi
4208: dth="16" data-view-component="true" class="octicon octicon-serve
4248: r">.    <path d="M1.75 1h12.5c.966 0 1.75.784 1.75 1.75v4c0 .372
4288: -.116.717-.314 1 .198.283.314.628.314 1v4a1.75 1.75 0 0 1-1.75 1
42c8: .75H1.75A1.75 1.75 0 0 1 0 12.75v-4c0-.358.109-.707.314-1a1.739 
4308: 1.739 0 0 1-.314-1v-4C0 1.784.784 1 1.75 1ZM1.5 2.75v4c0 .138.11
4348: 2.25.25.25h12.5a.25.25 0 0 0 .25-.25v-4a.25.25 0 0 0-.25-.25H1.7
4388: 5a.25.25 0 0 0-.25.25Zm.25 5.75a.25.25 0 0 0-.25.25v4c0 .138.112
43c8: .25.25.25h12.5a.25.25 0 0 0 .25-.25v-4a.25.25 0 0 0-.25-.25ZM7 4
4408: .75A.75.75 0 0 1 7.75 4h4.5a.75.75 0 0 1 0 1.5h-4.5A.75.75 0 0 1
4448:  7 4.75ZM7.75 10h4.5a.75.75 0 0 1 0 1.5h-4.5a.75.75 0 0 1 0-1.5Z
4488: M3 4.75A.75.75 0 0 1 3.75 4h.5a.75.75 0 0 1 0 1.5h-.5A.75.75 0 0
44c8:  1 3 4.75ZM3.75 10h.5a.75.75 0 0 1 0 1.5h-.5a.75.75 0 0 1 0-1.5Z
4508: "></path>.</svg>.</template>..<template id="globe-icon">.  <svg 
4548: aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1"
4588:  width="16" data-view-component="true" class="octicon octicon-gl
45c8: obe">.    <path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0ZM5.78 8.75a
4608: 9.64 9.64 0 0 0 1.363 4.177c.255.426.542.832.857 1.215.245-.296.
4648: 551-.705.857-1.215A9.64 9.64 0 0 0 10.22 8.75Zm4.44-1.5a9.64 9.6
4688: 4 0 0 0-1.363-4.177c-.307-.51-.612-.919-.857-1.215a9.927 9.927 0
46c8:  0 0-.857 1.215A9.64 9.64 0 0 0 5.78 7.25Zm-5.944 1.5H1.543a6.50
4708: 7 6.507 0 0 0 4.666 5.5c-.123-.181-.24-.365-.352-.552-.715-1.192
4748: -1.437-2.874-1.581-4.948Zm-2.733-1.5h2.733c.144-2.074.866-3.756 
4788: 1.58-4.948.12-.197.237-.381.353-.552a6.507 6.507 0 0 0-4.666 5.5
47c8: Zm10.181 1.5c-.144 2.074-.866 3.756-1.58 4.948-.12.197-.237.381-
4808: .353.552a6.507 6.507 0 0 0 4.666-5.5Zm2.733-1.5a6.507 6.507 0 0 
4848: 0-4.666-5.5c.123.181.24.365.353.552.714 1.192 1.436 2.874 1.58 4
4888: .948Z"></path>.</svg>.</template>..<template id="issue-opened-ic
48c8: on">.  <svg aria-hidden="true" height="16" viewBox="0 0 16 16" v
4908: ersion="1.1" width="16" data-view-component="true" class="octico
4948: n octicon-issue-opened">.    <path d="M8 9.5a1.5 1.5 0 1 0 0-3 1
4988: .5 1.5 0 0 0 0 3Z"></path><path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1
49c8:  8 0ZM1.5 8a6.5 6.5 0 1 0 13 0 6.5 6.5 0 0 0-13 0Z"></path>.</sv
4a08: g>.</template>..<template id="device-mobile-icon">.  <svg aria-h

4ea9: 
== Info: Connection #0 to host github.com left intact


```

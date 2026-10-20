# DreamCatcher packaging

Files for running mxl-fabrics-proxy on a DreamCatcher as a systemd service
instead of a container, built into a `mxl-fabrics-proxy` deb by the DC
server repo's `thirdparty/rdma/scripts/build-dc-mxl-fabrics-proxy-deb.sh`:

| File | Installed as |
|---|---|
| `mxl-fabrics-proxy.service` | `/usr/lib/systemd/system/mxl-fabrics-proxy.service` |
| `debian/control.in` | the deb's `DEBIAN/control` (`@VERSION@`, `@DEPENDS@` filled in at build) |
| `debian/postinst`, `debian/prerm` | the deb's maintainer scripts |

The deb also installs `mxl-fabrics-proxy`, `mxl-fabrics-proxy-reloader`
(Go, built with `CGO_ENABLED=0`) and `mxl-fabrics-proxy-worker` (C++,
`cmake --install`) to `/usr/bin` - the proxy starts the worker by name.

The service runs once `/opt/dreamcatcher/share/mxl/mxl-fabrics-proxy-config.yaml`
exists and listens on `0.0.0.0:2283`; override either in
`/etc/default/mxl-fabrics-proxy` (`MXL_FABRICS_PROXY_CONFIG`,
`MXL_FABRICS_PROXY_LISTEN`).

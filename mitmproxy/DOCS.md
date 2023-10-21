# Web UI

To access the user interface of mitmproxy, click 'open web UI' from the addon info page.
This connects to the 'mitmweb' service running within the addon.

# Configuration

The configuration for the mitmproxy can be done via the key-value pairs in the addon configuration.
Just add an new pair to the `options` array. _Please add all settings as strings!_

Example:

```yaml
options:
  - name: "anticache"
    value: "true"
  - name: "certs"
    value: "/ssl/mycert.pem"
```

The list with all possible settings can be found [here](https://docs.mitmproxy.org/stable/concepts-options/#available-options).

It is possible to modify settings via the user interface, but these are not
currently saved between restarts of the mitmproxy addon.

If you need to write into a file, the `/share` folder is mapped into the addon.

## Certificates

To access also the certificates of Home Assistant the `/ssl` folder is mapped in read-only.
Notice that mitmproxy requests the certificates as pem files.

### Own ca certificate

If you want your own ca signing the traffic the `custom_ca` option can be used.
For more about the ca certificate requirements see [here](https://docs.mitmproxy.org/stable/concepts-certificates/#ca-and-cert-files)

Example:

```yaml
options:
  - name: "anticache"
    value: "true"
custom_ca: /ssl/ca-cert.pem
```

## Fixed Settings

There are also a few settings which are fixed to their values. Those are:

- `web_host`
- `web_port`
- `listen_port`
- `confdir`

_Note that the listen port is configured as `8080` by default, this is the proxy server where the clients make their connection. Changing the setting in the addon config re-maps the internal port 8080 to the external port specified. mitmweb is unaware that this remapping is taking place, so it still displays `HTTP(S) proxy listening at _:8080`, regardless of what the external port setting is. Please ignore the '8080' shown on the mitmweb in this case.\*

# Onboarding

To install the mitmproxy certificate authority as a trusted CA, the onboarding page can be accessed via `http://mitm.it`. This is a magic URL - when your proxy settings are configured correctly and mitmproxy is running, mitmproxy will intercept this and show you a page to download the root certificates for https monitoring.

Follow the instructions on the page to install these to your device.

Notice that your traffic must be routed over mitmproxy to access the page.

# Development

Debugging and developing mitmproxy can be challenging when inside a container, especially the link between haproxy and mitmweb which can be hard to log and debug.

The following commands help expose this interaction to be running directly on the develoment machine. Each should be run in a parallel separate terminal.

Set up mitmproxy to expose the interception proxy port on 9080, and expose the web UI on 9090:
`docker run --rm -it -p 9080:8080 -p 9090:8081 mitmproxy/mitmproxy mitmweb --web-host 0.0.0.0`

Set up haproxy to run listenning on port 8082, mapping to 8081
`docker run -p 8082:8081 -v /home/dave/dev/home-assistant-addons/mitmproxy/root/etc/haproxy:/usr/local/etc/haproxy:ro --sysctl net.ipv4.ip_unprivileged_port_start=0 haproxy:2.3`

Explanation: the connection is then made in the following siquence

- web browser views http://localhost:8082
- (haproxy container:8082, mapped to internal :8081 )
- haproxy config file then defines the reverse proxy redirect 8081 to localhost:9090
- (mitmproxy mitmweb conatiner running on localhost:9090, mapped to internal: 8081 port serving web page)
- user sees content from mitmweb on their browser.

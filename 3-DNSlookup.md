# DNS lookup

_Context: Browser has determined what the HTTP/S request will look like. Now it needs to find the destination of the ``Host``. "What IP address is this HTTP request destined for?"_

_OSI Layer(s): 7_

* Browser checks if the host is in its cache.

* If not found, the browser calls ``gethostbyname`` library function (varies by OS) to do the lookup.

* ``gethostbyname`` checks if the hostname can be resolved by reference in the local ``hosts`` file (whose location `varies by OS`) before trying to resolve the hostname through DNS.

* If ``gethostbyname`` does not have it cached nor can find it in the ``hosts`` file then it makes a request to the DNS server configured in the network stack. This is typically the local router or the ISP's caching DNS server.

* If the DNS server is on the same subnet the network library follows the ``ARP process`` below for the DNS server.

* If the DNS server is on a different subnet, the network library follows the ``ARP process`` below for the default gateway IP.

_Demonstration Steps:_
  * Launch Chrome net-internals DNS config, clear DNS cache
  ``chrome://net-internals/#dns``
  * Check ``/etc/host`` file
  ```bash 
   cat /etc/hosts
  ```
  * clear DNS cache (cmd is for OSX)
  ```bash
  $ sudo killall -HUP mDNSResponder; say let us move on to address resolution protocol
  ```

[Next: ARP process](./4-ARPprocess.md)
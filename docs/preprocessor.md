# yasio Macros

The macros listed in the table below may be used to control the interface, functionality, and behaviour of `yasio`.  
You can define them at [yasio/detail/config.hpp](https://github.com/yasio/yasio/blob/master/yasio/detail/config.hpp) or compiler preprocessors.

|Name|Description|
|----------|-----------------|
|*YASIO_HAVE_KCP*|Whether enable kcp, default: `off`|
|*YASIO_HEADER_ONLY*|Whether enable header only, default: `off`|
|*YASIO_SSL_BACKEND*|Choose ssl backend, since 3.36.0<br/> `1`. Use OpenSSL<br/>`2`. Use mbedtls|
|*YASIO_ENABLE_UDS*|Whether enable unix domain socket support, current only unix-like system and win10 RS5 support this feature, default: `off`|
|*YASIO_HAVE_CARES*|Whether use c-ares to resolve domain name, default: `off`|
|*YASIO_VERBOSE_LOG*|Whether enable verbose log, default: `off`|
|*YASIO_NT_COMPAT_GAI*|Whether enable windows xp `getaddrinfo` API compatible, default: `off`|
|*YASIO_USE_SPSC_QUEUE*|Whether use SPSC queue, default: `off`|
|*YASIO_HAVE_HALF_FLOAT*|Whether enable half float, depends on [half.hpp](https://github.com/yasio/external/blob/master/half/half.hpp)|
|*YASIO_DISABLE_OBJECT_POOL*|Whether disable object pool|
|*YASIO_DISABLE_CONCURRENT_SINGLETON*|Whether disable concurrent singleton|
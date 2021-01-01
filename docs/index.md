# yasio Documentation

[![Release](https://img.shields.io/badge/release-v3.36.0-blue.svg)](https://github.com/yasio/yasio/releases)

*yasio is a multi-platform support c++11 library with focus on asio (asynchronous socket I/O) for any client application, support windows & linux & apple & android & win10-universal.*

* [yasio GitHub](https://github.com/yasio/yasio)
* yasio Documentation
  - [English](https://docs.yasio.org/en/latest/)
  - [简体中文](https://docs.yasio.org/zh_CN/latest/)

* Cross-platform:
  * Compiler: 
    - Visual Studio 2013+
    - GCC4.7+
    - xcode9+
    - Other C++11,14,17 Compilers

  * Architecture: x86, x64, ARM and etc.
  * OS: Windows, macOS, Linux, FreeBSD, iOS, Android And etc.

## Test case
This demo simply send http request to ``tool.chinaz.com`` and print resposne data.

=== "C++"
```cpp

  #include "yasio/yasio.hpp"
  #include "yasio/obstream.hpp"
  using namespace yasio;
  using namespace yasio::inet;
  
  int main()
  {
    io_service service({"tool.chinaz.com", 80});
    service.set_option(YOPT_S_DEFERRED_EVENT, 0); // 直接在网络线程分派网络事件
    service.start([&](event_ptr&& ev) {
      switch (ev->kind())
      {
        case YEK_PACKET: {
          auto packet = std::move(ev->packet());
          fwrite(packet.data(), packet.size(), 1, stdout);
          fflush(stdout);
          break;
        }
        case YEK_CONNECT_RESPONSE:
          if (ev->status() == 0)
          {
            auto transport = ev->transport();
            if (ev->cindex() == 0)
            {
              obstream obs;
              obs.write_bytes("GET /index.htm HTTP/1.1\r\n");
  
              obs.write_bytes("Host: tool.chinaz.com\r\n");
  
              obs.write_bytes("User-Agent: Mozilla/5.0 (Windows NT 10.0; "
                              "WOW64) AppleWebKit/537.36 (KHTML, like Gecko) "
                              "Chrome/87.0.4820.88 Safari/537.36\r\n");
              obs.write_bytes("Accept: */*;q=0.8\r\n");
              obs.write_bytes("Connection: Close\r\n\r\n");
  
              service.write(transport, std::move(obs.buffer()));
            }
          }
          break;
        case YEK_CONNECTION_LOST:
          printf("The connection is lost.\n");
          break;
      }
    });
    // open channel 0 as tcp client
    service.open(0, YCK_TCP_CLIENT);
    getchar();
  }
```

=== "Lua"
```lua
  local ip138 = "tool.chinaz.com"
  local service = yasio.io_service.new({host=ip138, port=80})
  local respdata = ""
  -- 传入网络事件处理函数启动网络服务线程，网络事件有: 消息包，连接响应，连接丢失
  service:start(function(ev)
          local k = ev.kind()
          if (k == yasio.YEK_PACKET) then
              respdata = respdata .. ev:packet():to_string()
          elseif k == yasio.YEK_CONNECT_RESPONSE then
              if ev:status() == 0 then -- status为0表示连接建立成功
                  local transport = ev:transport()
                  local obs = yasio.obstream.new()
                  obs:write_bytes("GET / HTTP/1.1\r\n")
  
                  obs:write_bytes("Host: " .. ip138 .. "\r\n")
  
                  obs:write_bytes("User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.117 Safari/537.36\r\n")
                  obs:write_bytes("Accept: */*;q=0.8\r\n")
                  obs:write_bytes("Connection: Close\r\n\r\n")
  
                  service:write(transport, obs)
              end
          elseif k == yasio.YEK_CONNECTION_LOST then
              print("request finish, respdata: " ..  respdata)
          end
      end)
  -- 将信道0作为TCP客户端打开，并向服务器发起异步连接，进行TCP三次握手
  service:open(0, yasio.YCK_TCP_CLIENT)
  
  -- 由于lua_State和渲染对象，不支持在其他线程操作，因此分派网络事件封装为全局Lua函数，并且以下函数应该在主线程或者游戏引擎渲染线程调用
  function gDispatchNetworkEvent(...)
      service:dispatch(128) -- 每帧最多处理128个网络事件
  end
  
  _G.yservice = service -- Store service to global table as a singleton instance
```

For more, please see [tests](https://github.com/yasio/yasio/tree/master/tests) & [examples](https://github.com/yasio/yasio/tree/master/tests):

* tests:

  * [echo_server](https://github.com/yasio/yasio/tree/master/tests/echo_server): TCP/UDP/KCP echo server
  * [echo_client](https://github.com/yasio/yasio/tree/master/tests/echo_client): TCP/UDP/KCP echo client
  * [ssltest](https://github.com/yasio/yasio/tree/master/tests/ssl): SSL client test, Get github.com home page
  * [tcptest](https://github.com/yasio/yasio/tree/master/tests/tcp): TCP test
  * [speedtest](https://github.com/yasio/yasio/tree/master/tests/speed): TCP,UDP,KCP local transfer
  * [mcast](https://github.com/yasio/yasio/tree/master/tests/mcast): multi-cast test program

* examples:

  * [ftp_server](https://github.com/yasio/ftp_server): A simple ftp server only support file download which is based on yasio，[click](ftp://ftp.yasio.org/) to visit.
  * [lua](https://github.com/yasio/yasio/tree/master/examples/lua): lua test contains http request，TCP unpack test code.
  * [xlua](https://github.com/yasio/xLua): Unity3D xlua Integration Demo.
  * [DemoUE4](https://github.com/yasio/DemoUE4): Unreal Engine 4 Integration Demo.

## Build tests & examples
* Ensure install compiler which support C++11, such as ``msvc``, ``gcc``, ``clang``
* Ensure ``git``, ``cmake`` installed
* Execude follow commands:

```sh
  git clone https://github.com/yasio/yasio
  cd yasio
  git submodule update --init --recursive 
  cd build
  # for xcode should be: cmake .. -GXcode
  cmake ..
  cmake --build . --config Debug
```

## API documentation
* [API References](api/index.md)
* [FAQ](faq.md)

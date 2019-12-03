# chrome-protocol-proxy

```chrome-protocol-proxy``` is small reverse websocket proxy designed for ```chrome debugging protocol```. It's purpose is to capture messages written to and received from [Chrome Debugging Protocol](https://chromedevtools.github.io/debugger-protocol-viewer), coalesce requests with responses, unpack messages from [Target domain](https://chromedevtools.github.io/debugger-protocol-viewer/tot/Target/) and provide easy to read, colored output. This tool is a fork of (and heavily inspired by) [chromedp-proxy](https://github.com/knq/chromedp/tree/master/cmd/chromedp-proxy).

![chrome-protocol-proxy screenshot](https://pbs.twimg.com/media/C9nifD2WsAEkl4s.jpg:large)

# Installation

## Via homebrew

```brew install wendigo/tap/chrome-protocol-proxy```

## Via go get

```go get -u github.com/wendigo/chrome-protocol-proxy```

# Features
- colored output,
- protocol frames filtering,🖖
- request-response coalescing,
- interprets [Target.sendMessageToTarget](https://chromedevtools.github.io/debugger-protocol-viewer/tot/Target/#method-sendMessageToTarget) requests,
- interprets [Target.receivedMessageFromTarget](https://chromedevtools.github.io/debugger-protocol-viewer/tot/Target/#event-receivedMessageFromTarget) responses and events with [sessionId](https://chromium.googlesource.com/chromium/src/+/237f82767da3bbdcd8d6ad3fa4449ef6a3fe8bd3),
- understands flatted sessions ([crbug.com/991325](crbug.com/991325))
- calculates and displays time delta between consecutive frames,
- writes logs and splits them based on connection id and target/session id.

# Usage
```
 Usage of chrome-protocol-proxy:
  -d	write logs file per session id
  -delta
    	show delta time between log entries
  -exclude value
    	exclude requests/responses/events matching pattern (default exclude = )
  -i	include request frames as they are sent
  -include value
    	display only requests/responses/events matching pattern (default include = )
  -l string
    	listen address (default "localhost:9223")
  -log-dir string
    	logs directory (default "logs")
  -m	display time in microseconds
  -once
    	debug single connection
  -q	do not show logs on stdout
  -r string
    	remote address (default "localhost:9222")
  -s	shorten requests and responses
  ```
  
# Demo
[![asciicast](https://asciinema.org/a/113947.png)](https://asciinema.org/a/113947?t=0:04&autoplay=1&speed=0.4)

# Tips & tricks

When using [Headless Chrome](https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md) navigate to [inspectable pages](http://localhost:9222/) and open inspector pane for url of your choosing. Then replace port in ```?ws=``` query param and point it to running ```chrome-protocol-proxy``` instance (default port is 9223). Now you're able to see what Chrome Debugger is exactly doing. Enjoy!

![headless chrome inspector traffic](https://pbs.twimg.com/media/C9nu8pIXsAE2Cpf.jpg:large)

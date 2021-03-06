# RansomCare
RansomCare is a crypto ransomware detection &amp; prevention software.

Currently it supports only **MacOS**, but its design aims to provide cross-platform support.

RansomCare is in its early stage, and everyone is welcome to extend it and port it to other platforms.

# Running
RansomCare
```bash
git clone https://github.com/Happyholic1203/ransomcare
cd ransomcare && sudo python run.py

# in another shell
open localhost:8888
```

With `http://localhost:8888` open in your browser, you'll be notified when crypto ransom events occur.

The suspicious process will be suspended when detected,
and you can then choose to kill the process or allow it to continue.

RansomCare doesn't have a UI yet, but you can inspect its status by:
```bash
curl http://localhost:8888/api/processes  # suspicious processes
curl http://localhost:8888/api/events  # detected crypto ransom events
```

# How it Works
RansomCare *sniffs* critical syscalls using [DTrace](http://dtrace.org/blogs/about/),
and it judges from process behaviors to see if it's a crypto ransomware.

Critical syscalls include: `open`, `getdirentries`, `read`, `write`, `close`, `unlink`.

Crypto ransomwares must perform the following syscalls in order to perform encryption to your files:

1. `getdirentries`: so it knows where and what the files are
2. `open`
3. `read`
4. `write`
5. `close` or `unlink`: `close` to overwrite the original file, `unlink` to write encrypted content to new file

# Tools that RansomCare Uses

## [DTrace](http://dtrace.org/blogs/about/)
RansomCare sniffs syscalls using [DTrace](http://dtrace.org/blogs/about/),
a tool that is included by default in various operating systems,
including Solaris, FreeBSD, and MacOS.

DTrace provides a variety of *probes*,
each of which can be used to trace different system events,
such as syscalls, io events, etc.

# Road Map

* Implement UI
* Support for Windows
* Implement whitelist

# Contribution

Please open issues if you encounter anything unpleasent.

Please send pull requests if you improved it.

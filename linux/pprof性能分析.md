# pprof

详细内容查看[go-pprof-practice](https://github.com/wolfogre/go-pprof-practice?tab=readme-ov-file)  



### 前置条件

**WSL安装 Google Chrome**

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb -O chrome.deb
sudo dpkg -i chrome.deb
sudo apt-get install -f
rm chrome.deb
```



### 🟢 场景一：在线实时采集

这种方式最常用。执行指令后，Go 会开始采样（比如 30 秒），采样完自动进入交互模式。

- **CPU 分析**（看哪最耗电/最吃算力）： `go tool pprof http://localhost:6060/debug/pprof/profile?seconds=30`
- **内存分析**（看谁占着内存不释放）： `go tool pprof http://localhost:6060/debug/pprof/heap`
- **阻塞/锁分析**（看程序卡在哪了）： `go tool pprof http://localhost:6060/debug/pprof/block` (或 `mutex`)

> **注意：** 即使是在线采集，`pprof` 也会悄悄在你本地 `~/pprof/` 目录下存一份副本（如 `pprof.main.samples.cpu.001.pb.gz`）。

```bash
# 交互终端
(pprof) top            # CPU 消耗 top10
(pprof) top -cum       # 累计 top10
(pprof) list <函数名>  # 查看函数详情
(pprof) web           # 图形化（需 Chrome + Graphviz）
(pprof) quit
```

------

### 🔵 场景二：离线查看（查看已保存的文件）

如果你已经下载好了 `.pb.gz` 文件，不需要再请求服务器，直接分析本地文件。

- **方式 A：Web 界面模式（最直观）** `go tool pprof -http=:8080 pprof.xxxx.pb.gz` *适合看：火焰图（Flame Graph）、调用拓扑图。*
- **方式 B：命令行交互模式（最快速）** `go tool pprof pprof.xxxx.pb.gz` *适合执行：`top`、`list`、`peek` 等命令。*

------

### 🟡 场景三：浏览器直接“裸看”（无需指令）

如果你不想输入任何 `go tool` 指令，直接在浏览器输入： `http://localhost:6060/debug/pprof/`

Usually, located at /usr/local/cuda/bin

## Non-Visual Profiler

```
$ nvprof python train_mnist.py
```

I prefer to use --print-gpu-trace.

```
$ nvprof --print-gpu-trace python train_mnist.py
```

## Visual Profiler

GPUを持っているホストで、

```
$ nvprof -o prof.nvvp python train_mnist.py
```

ローカルに持ってきて、

```
$ nvvp prof.nvvp
```

とやったほうが X11 Forwarding を使ったりするよりキビキビ動いて良い。

https://gist.githubusercontent.com/sonots/5abc0bccec2010ac69ff74788b265086/raw/eb11754de8c29bf721cd6049510dabfcaf84757b/nvvp.md
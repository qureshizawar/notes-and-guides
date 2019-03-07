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
## Let's do it!

In the environment:

Enter into this example folder:

```bash
cd ~/linux-observability-with-bpf/code/chapter-2/hello_world
```

Compile the program and the loader

```bash
make bpfload
```

It will create a BPF ELF named `bpf-program.o` and a Loader named `monitor-exec`.

Now you can execute the bpf program with root privileges and leave it running.

```
# ./monitor-exec
```

The program is made in a way that everytime an `execve` syscall is executed it prints `Hello, BPF World!`.

Now, open another terminal in the same machine and issue a command that does an `execve`, for example `ls` does.


```bash
ls
```

It should show something like this:

```
            bash-3309  [000] ....  2951.144342: 0: Hello, BPF World!
```

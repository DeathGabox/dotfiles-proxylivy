HDD

> Restablecer Low Level Format con [Badblock](https://wiki.archlinux.org/title/Badblocks#Read-write_test_(warning:_destructive)) !!DESTRUCTIVE!!
>
> Nota: Se puede demorar mucho
```
tune2fs -l dev/sdxX
badblocks -wsv -b Block Size /dev/device
```


SDD
Ni Idea, testeo cuando tenga uno :p

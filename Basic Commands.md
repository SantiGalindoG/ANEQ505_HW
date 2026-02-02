## Node for Friday
```

sinteractive --reservation=aneq505 --time=01:00:00 --partition=amilan --nodes=1 --ntasks=2 --qos=normal

```

## Node for every other day

```

ainteractive --time=01:00:00 --partition=amilan --nodes=1 --ntasks=2 --qos=normal

```

#### we first purge any loaded modules from the node we are on, this ensures no conflicting modules are "on"   
##### modules are preloaded packages of things people commonly use

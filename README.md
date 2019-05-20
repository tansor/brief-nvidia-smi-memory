# brief-nvidia-smi-memory
Feel free to watch nvidia-smi and memory usage !

```
 89C 100W  8533MiB/11178MiB  76%
 60C 252W 10429MiB/11175MiB  99%
 86C 161W 10189MiB/11178MiB  57%
Mem:      41702MiB/64371MiB  64%
Swp:        147MiB/32758MiB   0%
```

Just adding these to `~/.bashrc` and then `source ~/.bashrc`:

```
_watch_all() {
    nvidia-smi|grep Def|cut -c 8-11,20-24,35-43,45,47-54,60-64;
    free_m_result=$(free -m);
    curr_mem=$(echo "$free_m_result"| grep Mem | cut -c 26-31);
    total_mem=$(echo "$free_m_result" | grep Mem | cut -c 15-19);
    curr_swp=$(echo "$free_m_result" | grep Swap | cut -c 26-31);
    tatal_swp=$(echo "$free_m_result" | grep Swap | cut -c 15-19);
    printf 'Mem:      %5sMiB/%5sMiB%4i%%\n' $curr_mem $total_mem $((curr_mem*100/total_mem))
    printf 'Swp:      %5sMiB/%5sMiB%4i%%\n' $curr_swp $tatal_swp $((curr_swp*100/tatal_swp))
}
alias watch-all="watch -t bash -i -c '_watch_all'"
```

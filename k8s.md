# Run debug container

```bash
kubectl run --rm -ti \
--restart=Never \
--pod-running-timeout=1m \
--image="docker.io/busybox:1.36" \
--overrides='{"spec":{"containers":[{"name":"debug","image":"docker.io/busybox:1.36","tty":true,"stdin":true,"securityContext":{"runAsUser":666, "runAsGroup":666},"resources":{"limits":{"cpu":"1","memory":"500Mi","ephemeral-storage":"10Mi"},"requests":{"cpu":"1","memory":"500Mi","ephemeral-storage":"10Mi"}}}]}}' \
debug
```

# Evicting pods

```bash
# Enters into the pod to get the PID of the main process 
#(6 in our example)
$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
xxx      6     0  0 Mar23 ?        00:00:00 /bin/bash /entrypoint.sh
[...]

# Also into the pod, creates a loop which writes to the stdout : 
$ while true; do echo 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec et cursus dolor. Aliquam id libero porttitor, commodo ligula quis, facilisis ligula. Vestibulum vel commodo turpis. Nunc imperdiet risus turpis, a eleifend nisl cursus non. Suspendisse dignissim fringilla vehicula. Aliquam erat volutpat. Etiam vitae arcu tincidunt, fringilla leo quis, vulputate turpis. Mauris iaculis sagittis magna, non posuere quam condimentum ut. Nullam quis rhoncus est. Donec maximus purus velit, sed cursus ante facilisis varius. Curabitur euismod mattis efficitur.'; done >> /proc/6/fd/2
```
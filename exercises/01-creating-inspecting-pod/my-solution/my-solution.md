# Exercise 1

In this exercise, you will practice the creation of a new Pod in a namespace. Once created, you will inspect it, shell into it and run some operations inside of the container.

## Creating a Pod and Inspecting it

1. Create the namespace `ckad-prep`.
```bash
k create ns ckad-prep
```
2. In the namespace `ckad-prep` create a new Pod named `mypod` with the image `nginx:2.3.5`. Expose the port 80.
```bash
k run mypod -n ckad-prep --image=nginx:2.3.5 --port=80
```
3. Identify the issue with creating the container. Write down the root cause of issue in a file named `pod-error.txt`.
```bash
k describe po mypod -n ckad-prep | grep events -C5 > pod-error.txt
```
4. Change the image of the Pod to `nginx:1.15.12`.
```bash
k set image po mypod -n ckad-prep nginx=nginx:1.15.12
```
5. List the Pod and ensure that the container is running.
```bash
k get po -n ckad-prep
```
6. Log into the container and run the `ls` command. Write down the output. Log out of the container.
```bash
k exec mypod -n ckad-prep -- ls exit
```
7. Retrieve the IP address of the Pod `mypod`.
```bash
k get po mypod -n ckad-prep -o wide | grep -i ip
```
8. Run a temporary Pod using the image `busybox`, shell into it and run a `wget` command against the `nginx` Pod using port 80.
```bash
k run temp --image=busybox -it --rm --command -- wget ???
```
9. Render the logs of Pod `mypod`.
```bash
k logs mypod
```
10. Delete the Pod and the namespace.
```bash
k delete po mypod -n ckad-prep
k delete ns ckad-prep
```
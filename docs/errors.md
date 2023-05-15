# Common Errors
## 1. Dev container not opening properly on the first time
### Message on Terminal
```bash
[6294 ms] Start: Run: docker inspect --type container dc629ce7ee7b
[6414 ms] Error: Command failed: docker run --sig-proxy=false -a STDOUT -a STDERR --mount type=bind,source=/Users/ivanrulik/CODE/ros2_dev_container,target=/workspaces/ros2_dev_container,consistency=cached --mount type=volume,src=vscode,dst=/vscode -l devcontainer.local_folder=/Users/ivanrulik/CODE/ros2_dev_container -l devcontainer.config_file=/Users/ivanrulik/CODE/ros2_dev_container/.devcontainer/devcontainer.json -e DISPLAY=1 -e WAYLAND_DISPLAY= -e XDG_RUNTIME_DIR= -e PULSE_SERVER= -e LIBGL_ALWAYS_SOFTWARE=1 --network=host --cap-add=SYS_PTRACE --security-opt=seccomp:unconfined --security-opt=apparmor:unconfined --volume=/tmp/.X11-unix:/tmp/.X11-unix --volume=/mnt/wslg:/mnt/wslg --ipc=host --entrypoint /bin/sh vsc-ros2_dev_container-df507b15657988327cf272376c66a73783fb93c2df810e2fe3f884c937eeedc7 -c echo Container started
[6415 ms] trap "exit 0" 15
[6415 ms] exec "$@"
[6415 ms] while sleep 1 & wait $!; do :; done -
[6415 ms]     at Tse (/Users/ivanrulik/.vscode/extensions/ms-vscode-remote.remote-containers-0.292.0/dist/spec-node/devContainersSpecCLI.js:1946:3264)
[6415 ms]     at rO (/Users/ivanrulik/.vscode/extensions/ms-vscode-remote.remote-containers-0.292.0/dist/spec-node/devContainersSpecCLI.js:1946:3200)
[6415 ms]     at process.processTicksAndRejections (node:internal/process/task_queues:96:5)
[6416 ms]     at async Xse (/Users/ivanrulik/.vscode/extensions/ms-vscode-remote.remote-containers-0.292.0/dist/spec-node/devContainersSpecCLI.js:1961:2626)
[6416 ms]     at async vh (/Users/ivanrulik/.vscode/extensions/ms-vscode-remote.remote-containers-0.292.0/dist/spec-node/devContainersSpecCLI.js:1961:3741)
[6416 ms]     at async gae (/Users/ivanrulik/.vscode/extensions/ms-vscode-remote.remote-containers-0.292.0/dist/spec-node/devContainersSpecCLI.js:2092:10213)
[6416 ms]     at async mae (/Users/ivanrulik/.vscode/extensions/ms-vscode-remote.remote-containers-0.292.0/dist/spec-node/devContainersSpecCLI.js:2092:9954)
[6422 ms] Exit code 1
```
### Solution
Commented out this line: `("--volume=/mnt/wslg:/mnt/wslg",)` from thid file [.devcontainer/devcontainer.json](/.devcontainer/devcontainer.json)

## 2. Container GUI apps error (Mac OS)
### Message on Terminal
```bash
qt.qpa.xcb: could not connect to display 1
qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "" even though it was found.
This application failed to start because no Qt platform plugin could be initialized. Reinstalling the application may fix this problem.

Available platform plugins are: eglfs, linuxfb, minimal, minimalegl, offscreen, vnc, xcb.
```
### Solution
Based on this [GIST](https://gist.github.com/cschiewek/246a244ba23da8b9f0e7b11a68bf3285) the solution in this case could be sumarized to:
1. Install [XQuartz]( https://www.xquartz.org/)</p>
(optional) run `brew install --cask xquartz`
2. Enable X11 connections from localhost
   ```bash
   xhost +localhost
   ```
3. Modify the line `"DISPLAY": "${localEnv:0}"` on [.devcontainer/devcontainer.json](/.devcontainer/devcontainer.json)
4. Now the container based GUI apps will open under XQuartz
# wspace - Workspaces
This repo is for docker workspace containers.

## Primary
The primary container is the ubuntu one.  It uses a base Ubuntu 18.04 LTS and adds tools for:
- Ansible
- Boto 3
- aws-cli
- cf cli with cf local plug-in
- Additional plug-ins
    - usage-report: cf install-plugin 'Usage Report' -r CF-Community

This container expects for /root and /csaa to be mapped to relevant volumes.
An additional mapping to allow docker is performed as well /var/run/docker.sock

## Build
The following command will build the container image. The use for FORCE_UPGRADE will force an update from the package manager.
```
docker build --build-arg FORCE_UPGRADE="$(date +%F)" -t n01apl4385.tent.trt.csaa.pri/blairk/ubu-wspace ubuntu/

docker tag n01apl4385.tent.trt.csaa.pri/blairk/ubu-wspace n01apl4385.tent.trt.csaa.pri/blairk/ubu-wspace:<version number>
```

## Sample run command
`docker run --rm -ti -v /c/Users/gchkenn/docker/fs/root:/root -v /c/Users/gchkenn:/csaa bkcsaa/ubu-wspace`

A local powershell function may be defined to simplify this:
```
# define a function to start amazon-based workspace
function aw () { docker run --rm -ti bkcsaa/amz-wspace /bin/bash }
function uw () { docker run --rm -ti -v /var/run/docker.sock:/var/run/docker.sock -v /c/Users/gchkenn/docker/fs/root:/root -v /c/Users/gchkenn:/csaa bkcsaa/ubu-wspace /bin/bash }
PS C:\Users\gchkenn\docker\wspace>
```

so,
`> uw`
will start an Ubuntu-based workspace.

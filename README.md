# mdiff

This repo is for doc purpose for get info about how minikube and minishift differed.

# start Option

```
$ minikube start -h
Starts a local kubernetes cluster using VM. This command
assumes you have already installed one of the VM drivers: virtualbox/vmwarefusion/kvm/xhyve/hyperv.

Usage:
  minikube start [flags]

Flags:
      --apiserver-ips ipSlice          A set of apiserver IP Addresses which are used in the generated certificate for localkube/kubernetes.  This can be used if you want to make the apiserver available from outside the machine (default [])
      --apiserver-name string          The apiserver name which is used in the generated certificate for localkube/kubernetes.  This can be used if you want to make the apiserver available from outside the machine (default "minikubeCA")
      --apiserver-names stringArray    A set of apiserver names which are used in the generated certificate for localkube/kubernetes.  This can be used if you want to make the apiserver available from outside the machine
      --cache-images                   If true, cache docker images for the current bootstrapper and load them into the machine.
      --container-runtime string       The container runtime to be used
      --disable-driver-mounts          Disables the filesystem mounts provided by the hypervisors (vboxfs, xhyve-9p)
      --dns-domain string              The cluster dns domain name used in the kubernetes cluster (default "cluster.local")
      --extra-config ExtraOption       A set of key=value pairs that describe configuration that may be passed to different components.
		The key should be '.' separated, and the first part before the dot is the component to apply the configuration to.
		Valid components are: kubelet, apiserver, controller-manager, etcd, proxy, scheduler.
      --feature-gates string           A set of key=value pairs that describe feature gates for alpha/experimental features.
      --gpu                            Enable experimental NVIDIA GPU support in minikube (works only with kvm2 driver on Linux)
      --hyperkit-vpnkit-sock string    Location of the VPNKit socket used for networking. If empty, disables Hyperkit VPNKitSock, if 'auto' uses Docker for Mac VPNKit connection, otherwise uses the specified VSock.
      --hyperkit-vsock-ports strings   List of guest VSock ports that should be exposed as sockets on the host (Only supported on with hyperkit now).
      --keep-context                   This will keep the existing kubectl context and will create a minikube context.
      --kubernetes-version string      The kubernetes version that the minikube VM will use (ex: v1.2.3) 
 OR a URI which contains a localkube binary (ex: https://storage.googleapis.com/minikube/k8sReleases/v1.3.0/localkube-linux-amd64) (default "v1.10.0")
      --kvm-network string             The KVM network name. (only supported with KVM driver) (default "default")
      --mount                          This will start the mount daemon and automatically mount files into minikube
      --mount-string string            The argument to pass the minikube mount command on start (default "/home/prkumar:/minikube-host")
      --network-plugin string          The name of the network plugin
      --nfs-share strings              Local folders to share with Guest via NFS mounts (Only supported on with hyperkit now)
      --nfs-shares-root string         Where to root the NFS Shares (defaults to /nfsshares, only supported with hyperkit now) (default "/nfsshares")
      --uuid string                    Provide VM UUID to restore MAC address (only supported with Hyperkit driver).
      --xhyve-disk-driver string       The disk driver to use [ahci-hd|virtio-blk] (only supported with xhyve driver) (default "ahci-hd")

$ ./minishift start -h
Starts a local single-node OpenShift cluster.

All flags of this command can also be configured by setting corresponding environment variables or persistent configuration options.
For the former prefix the flag with MINISHIFT_, uppercase characters and replace '-' with '_', for example MINISHIFT_VM_DRIVER.
For the latter see 'minishift config -h'.

Usage:
  minishift start [flags]

Flags:
  -a, --addon-env stringSlice            Specify key-value pairs to be added to the add-on interpolation context.
      --extra-clusterup-flags string     Specify optional flags for use with 'cluster up' (unsupported)
  -h, --help                             help for start
      --http-proxy string                HTTP proxy in the format http://<username>:<password>@<proxy_host>:<proxy_port>. Overrides potential HTTP_PROXY setting in the environment.
      --https-proxy string               HTTPS proxy in the format https://<username>:<password>@<proxy_host>:<proxy_port>. Overrides potential HTTPS_PROXY setting in the environment.
      --network-nameserver stringSlice   Specify nameserver to use for the instance.
      --no-provision                     Do not provision the VM with OpenShift (experimental)
      --no-proxy string                  List of hosts or subnets for which no proxy should be used.
      --openshift-version string         The OpenShift version to run, eg. v3.9.0 (default "v3.9.0")
      --password string                  Password for the virtual machine registration.
      --public-hostname string           Public hostname of the OpenShift cluster.
      --registry-mirror stringSlice      Registry mirrors to pass to the Docker daemon.
      --remote-ipaddress string          IP address of the remote machine to provision OpenShift on
      --remote-ssh-key string            SSH private key location on the host to connect remote machine
      --remote-ssh-user string           The username of the remote machine to provision OpenShift on
      --routing-suffix string            Default suffix for the server routes.
      --server-loglevel int              Log level for the OpenShift server.
      --skip-registration                Skip the virtual machine registration.
      --skip-registry-check              Skip the Docker daemon registry check.
      --skip-startup-checks              Skip the startup checks.
      --username string                  Username for the virtual machine registration.
```

# Image cache Options

For minishift it is saved in OCI format and can be used by any container runtime.

- https://docs.okd.io/latest/minishift/using/image-caching.html

```
$ minishift images cache-config add <image_name>

$ minishift images list
openshift/origin-deployer:v3.9.0
openshift/origin-docker-registry:v3.9.0
openshift/origin-haproxy-router:v3.9.0
openshift/origin-pod:v3.9.0
openshift/origin-web-console:v3.9.0
openshift/origin:v3.9.0

$ ls ~/.minishift/cache/images/
blobs  index.json  oci-layout

$ ls ~/.minishift/cache/images/blobs/sha256/
04c0961c79a92e95f2b161220509afbdc47992aecf3314ddf02d61e4c34043d6  6185afec78483e38c8f5d0fc044767b2e8fb08102d7db0c2f6a1169de2dcaa9b
0530b896b578c43cb235ca8a7f77156fe71db42afe2daeb339d323a06f0a0c77  624682853ca731353fa5504d65271586b45e06eb840f03149d60ae36f9a87ce1
0ae899fbe36c0552576320fb61a588f315dfb059534458219ba7017d09f2628c  6b85d7aec983b06100aeafa02065c713fbb525c750089640cf8ac92ae3dac034
12a3f005312b5ca0af6d100baf639c8f3b1d816a87aa2d85fc80bba8f678e99e  b6128f1742e89123e0e7fd45cebbdeec0dfd9cf0f48d3bb807efe2997d593ff0
1e36a6179944244c75daff7c09c9bbe4ead48b2bb11efe610f87c8a589f55a5f  bcc97fbfc9e1a709f0eb78c1da59caeb65f43dc32cd5deeb12b8c1784e5b8237
234c7bed388fb8eaf5857442ab69b3b57a0d1ae659c7b7afa064d8df66cf7355  becbd3121d3d21e79ebad2a71940af0b9fb191992d3ca8549cbe31acce702987
2a24536ab4f4549f0fc947e92b7ae53fbf478c7b60d77dee7c90d004a64b9172  d288a07bf508bcbaa1108ee3809529ba20bf808813bf2c8a82aed6db460d0274
2d32bf3716ee731daef1353eff71510d70564fc6c7b89c9894d2dc8dfbec7c17  d398ba877ec784409eec8520c3be6cbe9d1b42cf897d7ea02b06954ac6f55e67
4a3e39ac32009c92c7cf55c574e8bccf91357b9c5a26340d8e78c5f56f9ecee2  e76efe9c84f2cde50c29a4b9bc0ee3cc32b7f08a0ebe7c5b37caca55734ed32f
562c234dab03310ffc3b3a1ad9c5dab37c3258a039376c837d3ed52f97a4e294  ff4bc504febafdb333402fa10295bc700dc027d9ba91a85d00e38970cc6fac6a
```

# Addon Options

For Minishift add-ons are directories that contain a text file with the .addon extension. The directory can also contain other resource files such as JSON template files. However, only one .addon file is allowed per add-on.

- https://docs.okd.io/latest/minishift/using/addons.html
- https://github.com/minishift/minishift-addons 

```
# Name: anyuid                                                                          
# Description: Allows authenticated users to run images under a non pre-allocated UID   
# Required-Vars: ACME_TOKEN                                                             
# OpenShift-Version: >3.6.0                                                             

mytoken := oc sa get-token oauth-client                                                 

oc new-app -p OPENSHIFT_OAUTH_CLIENT_SECRET=#{mytoken}                                  
oc adm policy add-scc-to-group anyuid system:authenticated 
```

# Hostfolder Options

Minishift support by default sshfs host folder mount out of box.

# ISO Options

Minishift have `CentOS` by default ISO.
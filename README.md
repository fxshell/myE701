# ![](https://www.lpice.eu/fileadmin/_processed_/csm_LPIC-DevOpsToolsEngineer_43de3c4735.jpg) myE701 - Exam 701: DevOps Tools Engineer 

Beispiel für einen Aufbau einer Dokumention des Lern- und Entwicklungsprozesses mit Ausgesuchten Unterkapiteln aus dem LPI E701 Exam
## Important Links
* [Module Overview](https://github.com/w901-fr19-mi/W901)
* [DevOps forked instructions](https://github.com/fxshell/E701---DevOps)
* [W901 BSCW](https://bscw.tbz.ch/bscw/bscw.cgi/26211645)
* [Docker in 12 minutes](https://www.youtube.com/watch?v=YFl2mCHdv24)
* [Docker compose in 12 minutes](https://www.youtube.com/watch?v=Qw9zlE3t8Ko)
* [docker-compose explained](https://www.youtube.com/watch?v=HUpIoF_conA)

<details> 
<summary> 
	
### How To: Dokumentation, Install etc. </summary>
	
## Dokumentation (Kapitel kann in der Kopie gelöscht werden)

Die Dokumentation erfolgt im Markdownformat, dem Standard Wiki Format von github. Dies geht am Einfachsten direkt auf github.com.

Eine Markdown Übersicht / Syntax etc. finden Sie auf:
* [Markdown Syntax inkl. Online Demo](http://markdown-syntax.de/Was-ist-Markdown/)
* [Dokumentation aus dem Modul M300](https://github.com/mc-b/M300/blob/master/80-Ergaenzungen/vcs/03-Markdown.md) 


## Installation (Kapitel kann in der Kopie gelöscht werden)

Hier lohnt es sich Vagrant zu verwenden. Damit kann gleichzeitig eine VM (Ubuntu 16.x) mit Docker und Kubernetes aufgesetzt werden oder mittels des Projektes [lernkube](https://github.com/mc-b/lernkube) ein Kubernetes Master. 

**Vagrant (lernkube) Installation**

Zuerst muss folgende SW Installiert werden:
* [Git/Bash](https://git-scm.com/downloads)
* [Vagrant](https://www.vagrantup.com/) 
* [VirtualBox](https://www.virtualbox.org/)

Wechseln Sie auf die Kommandozeile (*bash* oder *PowerShell*) und klonen des Projekt `lernkube` und erstellen die VM(s):

	git clone https://github.com/mc-b/lernkube
	cd lernkube
	cp templates/DUK.yaml config.yaml
	vagrant plugin install vagrant-disksize
	vagrant up

Während der Installation werden im Verzeichnis `lernkube` mehrere `.bat` Dateien und die Client Programme `docker`, `kubectl`, `helm` etc. erzeugt.

Die Bezeichnungen deren Funktion kann mittels `kubeps.bat` (*PowerShell*) oder `source kubeenv` (*Bash*) angezeigt werden. Die Scripts setzen gleichzeitig die Umgebungsvariablen, damit vom Notebook Docker und Kubernetes (`kubectl`) an die VM weitergereicht werden können.

Beispiele:

docker images # zeigt alle Container Images an
kubectl get all # zeigt alle Kubernetes Ressourcen an.

**Alternative Installationen** 

Alternativ kann [Docker for Windows/Mac](https://www.docker.com/products/docker-desktop) oder [Minikube](https://github.com/kubernetes/minikube) verwendet werden. Diese Umgebungen sind aber nicht Cluster fähig und erfordern [Feintuning](https://github.com/mc-b/lernkube/tree/master/docker4windows/).

Oder die gleiche Umgebung wie mit lernkube auf den Cloud Plattformen von Amazon und Microsoft eingerichtet werden.

* [Amazon AWS Cloud](https://github.com/mc-b/lernkube/tree/master/aws/) - hat noch Probleme mit Datenspeicherung und LoadBalancer.
* [Microsoft Azure Cloud](https://github.com/mc-b/lernkube/tree/master/azure/)	 

**Weitere nützliche Programme**

* [Windows SSH Client, putty](https://putty.org)
* [Grafischer Windows SFTP Client, Bitvise SSH Client](https://www.bitvise.com/ssh-client-download)
* [Visual Studio Code](https://code.visualstudio.com/)
</details>

## Fahrplan

| Datum | behandelte Unterrichtsinhalte: | Gewichtung |
| -------- | ------ | -------- |
| 15.05.19 | Linux Evolution and Popular Operating Systems | 2 |
| 15.05.19 | Installation SW, Einrichten Linux VM(s)<br>[701.1 Modern Software Development, 1. Teil](https://github.com/w901-fr19-mi/E701#7011-modern-software-development) | 6 |
| 22.05.19 | [701.1 Modern Software Development, 2. Teil](https://github.com/w901-fr19-mi/E701#7011-modern-software-development) | 4 |
| 29.05.19 | [701.3 Source Code Management](https://github.com/w901-fr19-mi/E701#7013-source-code-management) | 5 | 
| 05.06.19 | 702.1 Container Usage, 1. Teil | 7 |
| 12.06.19 | 702.1 Container Usage, 2. Teil | (7) |
| 19.06.19 | 702.2 Container Deployment and Orchestration | 5 |
| 26.06.19 | LB1 Theoretische Prüfung und Abschluss LB2 | - |
| 03.07.19 | Sommersporttage | - |
|          | Total Punkte | 27 (34) !

Kapitel aus E701 wurden in der Gruppe mit .... erarbeitet. Davon sind mindestens 14 Punkte selbständig erarbeitet worden. 

# Dokumention des Lern- und Entwicklungsprozesses
## Kapitel 1: Linux Basics recap (Status: In Arbeit)
[Linux Evolution and popular operating Systems](https://github.com/w901-fr19-mi/E010#11-linux-evolution-and-popular-operating-systems)

**Weight**: 2

**Beschreibung** Linux Überblick: Was ist Linux, was für Distro gibt es, was sind die Unterschiede, wie ist es Aufgebaut?

**Tagesziele** Überblick über das Modul erhalten, [Linux Essentials](https://www.tuxcademy.org/download/de/lxes/lxes-de-manual.pdf) überfliegen und interessante Passagen recherchieren/lösen & sowie gestellte Fragen beantworten

### Beispiele und Arbeitsergebnisse

#### Beef zwischen Torvaldis & Tannenbaum
Zu einer Zeit in der Computer schon Fuss gefasst hatten aber es immernoch ständig Änderungen gab beeften sich der Gründer von Linux (Linus Torvaldis) und der Gründer der Distibution Minix (Andrew S. Tanenbaum) öffentlich darüber welche Architektur (Monolithischer Kernel oder Microkernel) besser ist.

Da heute keiner Minix kennt und Linux das grösste Betriebsystem ist, ist die Antwort naheliegend.
***
#### Monolithic Kernel

*This article is an answer from Stackoverflow and only describes monolithic in contect with __operation systems__.*

*[Monolithischer Kernel](https://stackoverflow.com/questions/1806585/why-is-linux-called-a-monolithic-kernel)*
A monolithic kernel is a kernel where all services (file system, VFS, device drivers, etc) as well as core functionality (scheduling, memory allocation, etc.) are a tight knit group sharing the same space. This directly opposes a microkernel.

A microkernel prefers an approach where core functionality is isolated from system services and device drivers (which are basically just system services). For instance, VFS (virtual file system) and block device file systems (i.e. minixfs) are separate processes that run outside of the kernel's space, using IPC to communicate with the kernel, other services and user processes. In short, if it's a module in Linux, it's a service in a microkernel, indicating an isolated process.

Do not confuse the term modular kernel to be anything but monolithic. Some monolithic kernels can be compiled to be modular (e.g Linux), what matters is that the module is inserted to and runs from the same space that handles core functionality (kernel space).

The advantage to a microkernel is that any failed service can be easily restarted, for instance, there is no kernel halt if the root file system throws an abort. This can also be seen as a disadvantage, though, because it can hide pretty critical bugs (or make them seem not-so-critical, because the problem seems to continuously fix itself). It's seen as a big advantage in scenarios where you simply can't conveniently fix something once it has been deployed.

The disadvantage to a microkernel is that asynchronous IPC messaging can become very difficult to debug, especially if fibrils are implemented. Additionally, just tracking down a FS/write issue means examining the user space process, the block device service, VFS service, file system service and (possibly) the PCI service. If you get a blank on that, its time to look at the IPC service. This is often easier in a monolithic kernel. GNU Hurd suffers from these debugging problems (reference). I'm not even going to go into checkpointing when dealing with complex message queues. Microkernels are not for the faint of heart.

The shortest path to a working, stable kernel is the monolithic approach. Either approach can offer a POSIX interface, where the design of the kernel becomes of little interest to someone simply wanting to write code to run on any given design.
![Monolithischer Kernel](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/OS-structure2.svg/1200px-OS-structure2.svg.png "Monolithischer Kernel")


**Fazit und Aussicht** Ich habe schon einiges Über den Aufbau des Linux Kernels gelernt. Die Zeit war aber relativ knapp und ich werde Privat noch Zeit investieren müssen um mehr zu verstehen.

***
## Kapitel: 2 What is all this ?! (Status: In Arbeit)

**Weight**: Personal value

**Beschreibung** Short explaination of ~~all~~ most services used in combination with Kubernetes.

**Tagesziele**, Since I have to read and understand each of the services I can not estimate how long I am going to take for each service. I'll try to do all of them.

**Vorgehen**, Read guides about Docker, keep them as link and conclude the most valuable information as markdown sheet.

### Beispiele und Arbeitsergebnisse

#### Ansible

TEXT
TEXT TEXT
**Links:** 
+ [Microservices benefits ands challanges](https://www.cio.com/article/3201193/7-reasons-to-switch-to-microservices-and-5-reasons-you-might-not-succeed.html)
+ second one




** Common Commands

| Name                                 | Command                                                                |
|--------------------------------------+------------------------------------------------------------------------|
| Run curl test temporarily            | =kubectl run --rm mytest --image=yauritux/busybox-curl -it=            |
| Run wget test temporarily            | =kubectl run --rm mytest --image=busybox -it=                          |
| Run nginx deployment with 2 replicas | =kubectl run my-nginx --image=nginx --replicas=2 --port=80=            |
| Set namespace preference             | =kubectl config set-context <context_name> --namespace=<ns_name>=      |
| List pods with nodes info            | =kubectl get pod -o wide=                                              |
| List everything                      | =kubectl get all --all-namespaces=                                     |
| Get all services                     | =kubectl get service --all-namespaces=                                 |
| Show nodes with labels               | =kubectl get nodes --show-labels=                                      |
| Validate yaml file with dry run      | =kubectl create --dry-run --validate -f pod-dummy.yaml=                |
| Start a temporary pod for testing    | =kubectl run --rm -i -t --image=alpine test-$RANDOM -- sh=             |
| kubectl run shell command            | =kubectl exec -it mytest -- ls -l /etc/hosts=                          |
| Get system conf via configmap        | =kubectl -n kube-system get cm kubeadm-config -o yaml=                 |
| Get deployment yaml                  | =kubectl -n denny-websites get deployment mysql -o yaml=               |
| Explain resource                     | =kubectl explain pods=, =kubectl explain svc=                          |
| Watch pods                           | =kubectl get pods  -n wordpress --watch=                               |
| Query healthcheck endpoint           | =curl -L http://127.0.0.1:10250/healthz=                               |
| Open a bash terminal in a pod        | =kubectl exec -it storage sh=                                          |
| Check pod environment variables      | =kubectl exec redis-master-ft9ex env=                                  |
| Enable kubectl shell autocompletion  | =echo "source <(kubectl completion bash)" >>~/.bashrc=, and reload     |
| Use minikube dockerd in your laptop  | =eval $(minikube docker-env)=, No need to push docker hub any more     |
| Kubectl apply a folder of yaml files | =kubectl apply -R -f .=                                                |
| Get services sorted by name          | kubectl get services --sort-by=.metadata.name                          |
| Get pods sorted by restart count     | kubectl get pods --sort-by='.status.containerStatuses[0].restartCount' |
| List all container images            | [[https://github.com/dennyzhang/cheatsheet-kubernetes-A4/blob/master/list-all-images.sh#L14-L17][list-all-images.sh]]                                                     |
| kubeconfig skip tls verification     | [[https://github.com/dennyzhang/cheatsheet-kubernetes-A4/blob/master/skip-tls-verify.md][skip-tls-verify.md]]                                                     |
| Reference                            | [[https://github.com/kubernetes/kubernetes/tags][GitHub: kubernetes releases]]                                            |
| Reference                            | [[https://cheatsheet.dennyzhang.com/cheatsheet-minikube-A4][minikube cheatsheet]], [[https://cheatsheet.dennyzhang.com/cheatsheet-docker-A4][docker cheatsheet]], [[https://cheatsheet.dennyzhang.com/cheatsheet-openshift-A4][OpenShift CheatSheet]]           |

** Check Performance
| Name                                         | Command                                              |
|----------------------------------------------+------------------------------------------------------|
| Get node resource usage                      | =kubectl top node=                                   |
| Get pod resource usage                       | =kubectl top pod=                                    |
| Get resource usage for a given pod           | =kubectl top <podname> --containers=                 |
| List resource utilization for all containers | =kubectl top pod --all-namespaces --containers=true= |

** Resources Deletion
| Name                                    | Command                                                  |
|-----------------------------------------+----------------------------------------------------------|
| Delete pod                              | =kubectl delete pod/<pod-name> -n <my-namespace>=        |
| Delete pod by force                     | =kubectl delete pod/<pod-name> --grace-period=0 --force= |
| Delete pods by labels                   | =kubectl delete pod -l env=test=                         |
| Delete deployments by labels            | =kubectl delete deployment -l app=wordpress=             |
| Delete all resources filtered by labels | =kubectl delete pods,services -l name=myLabel=           |
| Delete resources under a namespace      | =kubectl -n my-ns delete po,svc --all=                   |
| Delete persist volumes by labels        | =kubectl delete pvc -l app=wordpress=                    |
| Delete statefulset only (not pods)      | =kubectl delete sts/<stateful_set_name> --cascade=false= |
#+BEGIN_HTML
<a href="https://cheatsheet.dennyzhang.com"><img align="right" width="185" height="37" src="https://raw.githubusercontent.com/dennyzhang/cheatsheet.dennyzhang.com/master/images/cheatsheet_dns.png"></a>
#+END_HTML
** Log & Conf Files
| Name                      | Comment                                                                   |
|---------------------------+---------------------------------------------------------------------------|
| Config folder             | =/etc/kubernetes/=                                                        |
| Certificate files         | =/etc/kubernetes/pki/=                                                    |
| Credentials to API server | =/etc/kubernetes/kubelet.conf=                                            |
| Superuser credentials     | =/etc/kubernetes/admin.conf=                                              |
| kubectl config file       | =~/.kube/config=                                                          |
| Kubernets working dir     | =/var/lib/kubelet/=                                                       |
| Docker working dir        | =/var/lib/docker/=, =/var/log/containers/=                                |
| Etcd working dir          | =/var/lib/etcd/=                                                          |
| Network cni               | =/etc/cni/net.d/=                                                         |
| Log files                 | =/var/log/pods/=                                                          |
| log in worker node        | =/var/log/kubelet.log=, =kubelet-proxy.log=                               |
| log in master node        | =kube-apiserver.log=, =kube-scheduler.log=, =kube-controller-manager.log= |
| Env                       | =/etc/systemd/system/kubelet.service.d/10-kubeadm.conf=                   |
| Env                       | export KUBECONFIG=/etc/kubernetes/admin.conf                              |
** Pod
| Name                         | Command                                                                                   |
|------------------------------+-------------------------------------------------------------------------------------------|
| List all pods                | =kubectl get pods=                                                                        |
| List pods for all namespace  | =kubectl get pods -all-namespaces=                                                        |
| List all critical pods       | =kubectl get -n kube-system pods -a=                                                      |
| List pods with more info     | =kubectl get pod -o wide=, =kubectl get pod/<pod-name> -o yaml=                           |
| Get pod info                 | =kubectl describe pod/srv-mysql-server=                                                   |
| List all pods with labels    | =kubectl get pods --show-labels=                                                          |
| List running pods            | kubectl get pods --field-selector=status.phase=Running                                    |
| Get Pod initContainer status | =kubectl get pod --template '{{.status.initContainerStatuses}}' <pod-name>=               |
| kubectl run command          | kubectl exec -it -n "$ns" "$podname" -- sh -c "echo $msg >>/dev/err.log"                  |
| Watch pods                   | =kubectl get pods  -n wordpress --watch=                                                  |
| Get pod by selector          | kubectl get pods --selector="app=syslog" -o jsonpath='{.items[*].metadata.name}'          |
| List pods and images         | kubectl get pods -o='custom-columns=PODS:.metadata.name,Images:.spec.containers[*].image' |
| List pods and containers     | -o='custom-columns=PODS:.metadata.name,CONTAINERS:.spec.containers[*].name'               |
| Reference                    | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                                                           |
** Label & Annontation
| Name                             | Command                                                           |
|----------------------------------+-------------------------------------------------------------------|
| Filter pods by label             | =kubectl get pods -l owner=denny=                                 |
| Manually add label to a pod      | =kubectl label pods dummy-input owner=denny=                      |
| Remove label                     | =kubectl label pods dummy-input owner-=                           |
| Manually add annonation to a pod | =kubectl annotate pods dummy-input my-url=https://dennyzhang.com= |
** Deployment & Scale
| Name                         | Command                                                                  |
|------------------------------+--------------------------------------------------------------------------|
| Scale out                    | =kubectl scale --replicas=3 deployment/nginx-app=                        |
| online rolling upgrade       | =kubectl rollout app-v1 app-v2 --image=img:v2=                           |
| Roll backup                  | =kubectl rollout app-v1 app-v2 --rollback=                               |
| List rollout                 | =kubectl get rs=                                                         |
| Check update status          | =kubectl rollout status deployment/nginx-app=                            |
| Check update history         | =kubectl rollout history deployment/nginx-app=                           |
| Pause/Resume                 | =kubectl rollout pause deployment/nginx-deployment=, =resume=            |
| Rollback to previous version | =kubectl rollout undo deployment/nginx-deployment=                       |
| Reference     | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]], [[https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#pausing-and-resuming-a-deployment][Link: Pausing and Resuming a Deployment]] |
#+BEGIN_HTML
<a href="https://cheatsheet.dennyzhang.com"><img align="right" width="185" height="37" src="https://raw.githubusercontent.com/dennyzhang/cheatsheet.dennyzhang.com/master/images/cheatsheet_dns.png"></a>
#+END_HTML
** Quota & Limits & Resource
| Name                          | Command                                                                 |
|-------------------------------+-------------------------------------------------------------------------|
| List Resource Quota           | =kubectl get resourcequota=                                             |
| List Limit Range              | =kubectl get limitrange=                                                |
| Customize resource definition | =kubectl set resources deployment nginx -c=nginx --limits=cpu=200m=     |
| Customize resource definition | =kubectl set resources deployment nginx -c=nginx --limits=memory=512Mi= |
| Reference                     | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                                         |
** Service
| Name                            | Command                                                                           |
|---------------------------------+-----------------------------------------------------------------------------------|
| List all services               | =kubectl get services=                                                            |
| List service endpoints          | =kubectl get endpoints=                                                           |
| Get service detail              | =kubectl get service nginx-service -o yaml=                                       |
| Get service cluster ip          | kubectl get service nginx-service -o go-template='{{.spec.clusterIP}}'            |
| Get service cluster port        | kubectl get service nginx-service -o go-template='{{(index .spec.ports 0).port}}' |
| Expose deployment as lb service | =kubectl expose deployment/my-app --type=LoadBalancer --name=my-service=          |
| Expose service as lb service    | =kubectl expose service/wordpress-1-svc --type=LoadBalancer --name=ns1=           |
| Reference                       | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                                                   |
** Secrets
| Name                        | Command                                                               |
|-----------------------------+-----------------------------------------------------------------------|
| List secrets                | =kubectl get secrets --all-namespaces=                                |
| Generate secret             | =echo -n 'mypasswd'=, then redirect to =base64 -decode=               |
| Create secret from cfg file | kubectl create secret generic db-user-pass --from-file=./username.txt |
| Reference                   | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]], [[https://kubernetes.io/docs/concepts/configuration/secret/][Link: Secrets]]                        |
** StatefulSet
| Name                               | Command                                                  |
|------------------------------------+----------------------------------------------------------|
| List statefulset                   | =kubectl get sts=                                        |
| Delete statefulset only (not pods) | =kubectl delete sts/<stateful_set_name> --cascade=false= |
| Scale statefulset                  | =kubectl scale sts/<stateful_set_name> --replicas=5=     |
| Reference           | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                          |
** Volumes & Volume Claims
| Name                      | Command                                                      |
|---------------------------+--------------------------------------------------------------|
| List storage class        | =kubectl get storageclass=                                   |
| Check the mounted volumes | =kubectl exec storage ls /data=                              |
| Check persist volume      | =kubectl describe pv/pv0001=                                 |
| Copy local file to pod    | =kubectl cp /tmp/my <some-namespace>/<some-pod>:/tmp/server= |
| Copy pod file to local    | =kubectl cp <some-namespace>/<some-pod>:/tmp/server /tmp/my= |
| Reference  | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                              |
** Events & Metrics
| Name                            | Command                                                    |
|---------------------------------+------------------------------------------------------------|
| View all events                 | =kubectl get events --all-namespaces=                      |
| List Events sorted by timestamp | kubectl get events --sort-by=.metadata.creationTimestamp   |
** Node Maintenance
| Name                                      | Command                       |
|-------------------------------------------+-------------------------------|
| Mark node as unschedulable                | =kubectl cordon $NDOE_NAME=   |
| Mark node as schedulable                  | =kubectl uncordon $NDOE_NAME= |
| Drain node in preparation for maintenance | =kubectl drain $NODE_NAME=    |
** Namespace & Security
| Name                          | Command                                                           |
|-------------------------------+-------------------------------------------------------------------|
| List authenticated contexts   | =kubectl config get-contexts=, =~/.kube/config=                   |
| Set namespace preference      | =kubectl config set-context <context_name> --namespace=<ns_name>= |
| Load context from config file | =kubectl get cs --kubeconfig kube_config.yml=                     |
| Switch context                | =kubectl config use-context <cluster-name>=                       |
| Delete the specified context  | =kubectl config delete-context <cluster-name>=                    |
| List all namespaces defined   | =kubectl get namespaces=                                          |
| List certificates             | =kubectl get csr=                                                 |
| Reference                     | [[https://cheatsheet.dennyzhang.com/kubernetes-yaml-templates][Link: kubernetes yaml templates]]                                   |
** Network
| Name                              | Command                                                  |
|-----------------------------------+----------------------------------------------------------|
| Temporarily add a port-forwarding | =kubectl port-forward redis-izl09 6379=                  |
| Add port-forwaring for deployment | =kubectl port-forward deployment/redis-master 6379:6379= |
| Add port-forwaring for replicaset | =kubectl port-forward rs/redis-master 6379:6379=         |
| Add port-forwaring for service    | =kubectl port-forward svc/redis-master 6379:6379=        |
| Get network policy                | =kubectl get NetworkPolicy=                              |
** Patch
| Name                          | Summary                                                               |
|-------------------------------+-----------------------------------------------------------------------|
| Patch service to loadbalancer | =kubectl patch svc $svc_name -p '{"spec": {"type": "LoadBalancer"}}'= |
** Extenstions
| Name                         | Summary                    |
|------------------------------+----------------------------|
| List api group               | =kubectl api-versions=     |
| List all CRD                 | =kubectl get crd=          |
| List storageclass            | =kubectl get storageclass= |
| List all supported resources | =kubectl api-resources=    |
#+BEGIN_HTML
<a href="https://cheatsheet.dennyzhang.com"><img align="right" width="185" height="37" src="https://raw.githubusercontent.com/dennyzhang/cheatsheet.dennyzhang.com/master/images/cheatsheet_dns.png"></a>
#+END_HTML
** Components & Services
*** Services on Master Nodes
| Name                    | Summary                                                                                                |
|-------------------------+--------------------------------------------------------------------------------------------------------|
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-apiserver][kube-apiserver]]          | exposes the Kubernetes API from master nodes                                                           |
| [[https://coreos.com/etcd/][etcd]]                    | reliable data store for all k8s cluster data                                                           |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-scheduler][kube-scheduler]]          | schedule pods to run on selected nodes                                                                 |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-controller-manager][kube-controller-manager]] | node controller, replication controller, endpoints controller, and service account & token controllers |
*** Services on Worker Nodes
| Name              | Summary                                                                                   |
|-------------------+-------------------------------------------------------------------------------------------|
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kubelet][kubelet]]           | makes sure that containers are running in a pod                                           |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-proxy][kube-proxy]]        | perform connection forwarding                                                             |
| [[https://github.com/docker/engine][Container Runtime]] | Kubernetes supported runtimes: Docker, rkt, runc and any [[https://github.com/opencontainers/runtime-spec][OCI runtime-spec]] implementation. |

*** Addons: pods and services that implement cluster features
| Name                          | Summary                                                                   |
|-------------------------------+---------------------------------------------------------------------------|
| DNS                           | serves DNS records for Kubernetes services                                |
| Web UI                        | a general purpose, web-based UI for Kubernetes clusters                   |
| Container Resource Monitoring | collect, store and serve container metrics                                |
| Cluster-level Logging         | save container logs to a central log store with search/browsing interface |

*** Tools
| Name                  | Summary                                                     |
|-----------------------+-------------------------------------------------------------|
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kubectl][kubectl]]               | the command line util to talk to k8s cluster                |
| [[https://github.com/kubernetes/kubernetes/tree/master/cmd/kubeadm][kubeadm]]               | the command to bootstrap the cluster                        |
| [[https://kubernetes.io/docs/reference/setup-tools/kubefed/kubefed/][kubefed]]               | the command line to control a Kubernetes Cluster Federation |
| Kubernetes Components | [[https://kubernetes.io/docs/concepts/overview/components/][Link: Kubernetes Components]]                                 |

**Fazit und Aussicht**, z.B. Die Durcharbeitung von ... gab mir ein besseres Verständnis über die Funktionsweise von Containern.

## Kapitel: 702.1 Container Usage (Status: In Arbeit)

**Weight**: 7 (7)

**Beschreibung** Gegenüberstellung welche Linux Technologien für Container verwendet werden.

**Tagesziele**, z.B. Erstellung einer Tabelle Linux - Container. 

**Vorgehen**, z.B. Studieren Background Linux Namespaces vs. Container, UnionFS vs. Container Layer, Unix Prozesse (Jobs) vs. Docker run/start/stop

**Beispiele und Arbeitsergebnisse**

| Linux          | Container      | Beschreibung      |
| -------------- | -------------- | ----------------- |
| Namespaces     | laufender Container | beim Starten des Containers wird in eine andere Linux Namespace gewechselt |
| UnionFS        | Image Layer         | Container Verwenden UnionFileSysteme um .... |
| Unix Prozesse  | run/start/stop      | docker run/start/stop Befehle ähneln dem .... Subsystem |

**Fazit und Aussicht**, z.B. Die Durcharbeitung von ... gab mir ein besseres Verständnis über die Funktionsweise von Containern.

## 


* [Exam 701: DevOps Tools Engineer](https://www.lpi.org/our-certifications/exam-701-objectives) 
* [E701 Dokumentation](https://github.com/w901-fr19-mi/E701)
* [myE701 Original Repository](https://github.com/w901-fr19-mi/myE701) 


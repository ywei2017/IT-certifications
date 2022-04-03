# CKA - Certified Kubernetes Administrator
# Why CKA
As of late 2021, we have been using Pivotal Cloud Foundry (PCF) since 2017. PCF works great, but there is more
momentum to migrate to k8s eventually. So the time has come to study up on k8s.

# The Journey
* I started in July 2021 hoping to complete the certification in the year. I created the home lab on the 8 
  year old Acer laptop with KVM, but lost focus shortly.
* January 2022, I decided - this time I will do it.
* 2022/3/24: Finished reading through k8s docs, tasks, and most tutorials.  Also finished the
  "Certified Kubernetes Administrator (CKA) Study Guide" by Benjamin Muschko (O'reilly).  I found the
  book is concise and well tailored. The practice is also good.  Next stage is to practice on 
  those concepts and prepare for the exam.
* 2022/3/26: Completed the [CKA-StudyGuide](https://github.com/David-VTUK/CKA-StudyGuide)
* 2022/3/27: Registered on the Linux Foundation for the exam. **I wished I did this earlier**, the 
  registration process tells a lot about the exam.
* 2022/3/27: Completed the [CKAD-exercises](https://github.com/dgkanatsios/CKAD-exercises)
* 2022/3/27: Completed the [cka-practice-test-1](https://prabhatsharma.in/blog/cka-practice-test-1)
* 2022/4/01: Completed the [cka-practice-test-2](https://prabhatsharma.in/blog/cka-practice-test-2)
* 2022/4/02-03: Did the first simulator test. I could do most of the questions, but took me twice as long.
  I did better on the complex ones, and tripped on more of the simple tasks.
* 2022/4/03: Did the [killercode/killer-shell-cka](https://killercoda.com/killer-shell-cka) exercises.
  They are nice practice scenarios, using the same killer.sh environment.
* 2022/4/06: Did the [bmuschko/cka-crash-course](https://github.com/bmuschko/cka-crash-course) exercises.
* 2022/4/09: Glanced through the Benjamin Muschko book again and did the excercies. Instead of taking days,
  this time it only takes a a few hours.
* 2022/4/10: Final refresh up on some of more difficult topics
* 2022/4/11: Took the exam. I took the day off, and glad I did so. After the exam, I was exhausted pretty much
  for the day. I found I have enough time, and again the difficult tasks are easier.


# Things to Know
* What Linux system is used for CKA? Ubuntu 20.0.4 as of April 2021. This sounds trivial, but different 
  Linux system can be appreciably different (`apt-get vs yum`). No windows stuff is involved.
* [killer.sh](https://killer.sh/) is the test environment. 

# Preparation Strategy
The Journey is basically what I did. 
* Read the docs and concepts to get a gauge how long it will take to get ready, realisticly.  In my case,
  the concepts are not new, since I have been managing the PCF platform since 2017. They just manifest
  in a different way.
* Do some practice. The more the better, and there are tons of resources on the web.
* Register for the exam, so you have access to the simulators. You can reschedule your actual exam to a later 
  date if you need more time. The simulator test is **VERY, VERY helpful**. If I do it againt, the biggest 
  change is to register earlier.
* Take the simulator test
* Prepare more if necessary
* Take the test

# Tech Tips
## Hard Concepts
These take more reading and practicing to get good handle on
* Taint node, toleration, nodeSelector (especially with empty value)
* Node affinity and pod affinity/anti-affinity
* topologySpreadConstraints
* RBAC: Use “api group”, NOT version. For example, “batch”, instead of “batch/v1”
* Role/Clusterrole for RoleBinding vs ClusterRoleBinding
* etcd snapshot save and restore, make sure you update the correct place in the static pod spec. I was
  tripped over by it multiple times.
* `grep -A 3`, `grep -C 5`, - never used it before
* `--record` to record the action, but
  `Flag --record has been deprecated, --record will be removed in the future`
* `k replace -f yaml --force` to update an existing resource
* Find all the systemd services by name, `find /etc/systemd/system/ | grep kube`

## Items to practice:
* Create role and rolebinding in command line (instead of yml)

## Someting to bear in mind
* `--show-labels`
* Many `kubectl` commands take `-o yaml`,  `-o wide`, `-o name`, `-o jsonpath` flags
* Don't like `yq`? Try `cat file | yq eval | jq`
* `Kubectl cp` to copy files to/from containers
* How do you *kill*  a pod? You `delete` it
* `crictl inspect` since dockershim is gone
* `Journalctl -u kubelet` to see kubelet extended logs
* `kubeadm token create --print-join-command` to create tokens to join new nodes
* If you define egress policy, do not forget DNS (tcp/udp port 53), otherwise the pod can't resolve
  hostnames.

# Test Tips
Pay more focus on high weight questions -- they have different weights.

The biggest confusion I had during the simulator test is to understand the intent. For example,

> Write a command listing all the pod names to `/opt/course1/p1/pod.sh`
>
>     cat /opt/course1/p1/pod.sh
>     kubectl get pod -o name

So the question is for the actual command, not the output (the `.sh` extension of the file). Also it
specifically asks for the pod **names**.

> Find the taints of node `cluster1-master1` and record in  `/opt/course1/p2/taints.txt`
>
>     cat /opt/course1/p2/taints.txt
>     node-role.kubernetes.io/master:NoSchedule
>

Also, `[]` is suppoed to be removed
> Find the master hostname, and record in 
>
>     # /opt/course/3/master.txt
>     hostname: [name] 
and it should be
>
>     # /opt/course/3/master.txt
>     hostname: master1

## Other Test Tips
* `export dr="--dry-run=client -o yaml”`
* `alias kn="kubectl -n namespace”`, for the *namespace* in that question, so you don't need keep on doing 
   `-n namespace`
* `ssh host "command” >> target`, it does all without asking for passwords
* partial credits of a question? The internet said yes.
* `mkdir p{1..25}`, and work on a single folder for each question, in case you need to come back and rework 
  on them. This helps keep things separate

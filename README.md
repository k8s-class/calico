# calico
Calico Network Isolation App

* Here is an example of a production app

$ git clone https://github.com/projectcalico/calico.git

$ cd calico/v2.0/getting-started/kubernetes/tutorials/stars-policy

$ kubectl create -f manifests/

* Wait for all the containers to come up

$ kubectl get pods --all-namespaces --watch

* Now you should be able to go to nodeip_address_any:30002 and see the network traffic

* Enable isolation

$ kubectl annotate ns stars "net.beta.kubernetes.io/network-policy={\"ingress\":{\"isolation\":\"DefaultDeny\"}}"
$ kubectl annotate ns client "net.beta.kubernetes.io/network-policy={\"ingress\":{\"isolation\":\"DefaultDeny\"}}"

* Allow access from the management UI.
$ kubectl create -f policies/allow-ui.yaml
$ kubectl create -f policies/allow-ui-client.yaml

* Allow traffic from the frontend to the backend

$ kubectl create -f policies/backend-policy.yaml

* Expose the frontend service to the client namespace

$ kubectl create -f policies/frontend-policy.yaml

* Now go into the AWS console and select the security group for the master node and add port 30002

* Go back to the webpage and check out the network traffic on nod_ip_any:30002

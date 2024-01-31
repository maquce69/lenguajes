OpenShift CLI (oc) administrator commands
oc adm build-chain
Output the inputs and dependencies of your builds

Example usage

  # Build the dependency tree for the 'latest' tag in <image-stream>
  oc adm build-chain <image-stream>

  # Build the dependency tree for the 'v2' tag in dot format and visualize it via the dot utility
  oc adm build-chain <image-stream>:v2 -o dot | dot -T svg -o deps.svg

  # Build the dependency tree across all namespaces for the specified image stream tag found in the 'test' namespace
  oc adm build-chain <image-stream> -n test --all
oc adm catalog mirror
Mirror an operator-registry catalog

Example usage

  # Mirror an operator-registry image and its contents to a registry
  oc adm catalog mirror quay.io/my/image:latest myregistry.com

  # Mirror an operator-registry image and its contents to a particular namespace in a registry
  oc adm catalog mirror quay.io/my/image:latest myregistry.com/my-namespace

  # Mirror to an airgapped registry by first mirroring to files
  oc adm catalog mirror quay.io/my/image:latest file:///local/index
  oc adm catalog mirror file:///local/index/my/image:latest my-airgapped-registry.com

  # Configure a cluster to use a mirrored registry
  oc apply -f manifests/imageContentSourcePolicy.yaml

  # Edit the mirroring mappings and mirror with "oc image mirror" manually
  oc adm catalog mirror --manifests-only quay.io/my/image:latest myregistry.com
  oc image mirror -f manifests/mapping.txt

  # Delete all ImageContentSourcePolicies generated by oc adm catalog mirror
  oc delete imagecontentsourcepolicy -l operators.openshift.org/catalog=true
oc adm certificate approve
Approve a certificate signing request

Example usage

  # Approve CSR 'csr-sqgzp'
  oc adm certificate approve csr-sqgzp
oc adm certificate deny
Deny a certificate signing request

Example usage

  # Deny CSR 'csr-sqgzp'
  oc adm certificate deny csr-sqgzp
oc adm cordon
Mark node as unschedulable

Example usage

  # Mark node "foo" as unschedulable
  oc adm cordon foo
oc adm create-bootstrap-project-template
Create a bootstrap project template

Example usage

  # Output a bootstrap project template in YAML format to stdout
  oc adm create-bootstrap-project-template -o yaml
oc adm create-error-template
Create an error page template

Example usage

  # Output a template for the error page to stdout
  oc adm create-error-template
oc adm create-login-template
Create a login template

Example usage

  # Output a template for the login page to stdout
  oc adm create-login-template
oc adm create-provider-selection-template
Create a provider selection template

Example usage

  # Output a template for the provider selection page to stdout
  oc adm create-provider-selection-template
oc adm drain
Drain node in preparation for maintenance

Example usage

  # Drain node "foo", even if there are pods not managed by a replication controller, replica set, job, daemon set or stateful set on it
  oc adm drain foo --force

  # As above, but abort if there are pods not managed by a replication controller, replica set, job, daemon set or stateful set, and use a grace period of 15 minutes
  oc adm drain foo --grace-period=900
oc adm groups add-users
Add users to a group

Example usage

  # Add user1 and user2 to my-group
  oc adm groups add-users my-group user1 user2
oc adm groups new
Create a new group

Example usage

  # Add a group with no users
  oc adm groups new my-group

  # Add a group with two users
  oc adm groups new my-group user1 user2

  # Add a group with one user and shorter output
  oc adm groups new my-group user1 -o name
oc adm groups prune
Remove old OpenShift groups referencing missing records from an external provider

Example usage

  # Prune all orphaned groups
  oc adm groups prune --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Prune all orphaned groups except the ones from the blacklist file
  oc adm groups prune --blacklist=/path/to/blacklist.txt --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Prune all orphaned groups from a list of specific groups specified in a whitelist file
  oc adm groups prune --whitelist=/path/to/whitelist.txt --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Prune all orphaned groups from a list of specific groups specified in a whitelist
  oc adm groups prune groups/group_name groups/other_name --sync-config=/path/to/ldap-sync-config.yaml --confirm
oc adm groups remove-users
Remove users from a group

Example usage

  # Remove user1 and user2 from my-group
  oc adm groups remove-users my-group user1 user2
oc adm groups sync
Sync OpenShift groups with records from an external provider

Example usage

  # Sync all groups with an LDAP server
  oc adm groups sync --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Sync all groups except the ones from the blacklist file with an LDAP server
  oc adm groups sync --blacklist=/path/to/blacklist.txt --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Sync specific groups specified in a whitelist file with an LDAP server
  oc adm groups sync --whitelist=/path/to/whitelist.txt --sync-config=/path/to/sync-config.yaml --confirm

  # Sync all OpenShift groups that have been synced previously with an LDAP server
  oc adm groups sync --type=openshift --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Sync specific OpenShift groups if they have been synced previously with an LDAP server
  oc adm groups sync groups/group1 groups/group2 groups/group3 --sync-config=/path/to/sync-config.yaml --confirm
oc adm inspect
Collect debugging data for a given resource

Example usage

  # Collect debugging data for the "openshift-apiserver" clusteroperator
  oc adm inspect clusteroperator/openshift-apiserver

  # Collect debugging data for the "openshift-apiserver" and "kube-apiserver" clusteroperators
  oc adm inspect clusteroperator/openshift-apiserver clusteroperator/kube-apiserver

  # Collect debugging data for all clusteroperators
  oc adm inspect clusteroperator

  # Collect debugging data for all clusteroperators and clusterversions
  oc adm inspect clusteroperators,clusterversions
oc adm migrate template-instances
Update template instances to point to the latest group-version-kinds

Example usage

  # Perform a dry-run of updating all objects
  oc adm migrate template-instances

  # To actually perform the update, the confirm flag must be appended
  oc adm migrate template-instances --confirm
oc adm must-gather
Launch a new instance of a pod for gathering debug information

Example usage

  # Gather information using the default plug-in image and command, writing into ./must-gather.local.<rand>
  oc adm must-gather

  # Gather information with a specific local folder to copy to
  oc adm must-gather --dest-dir=/local/directory

  # Gather audit information
  oc adm must-gather -- /usr/bin/gather_audit_logs

  # Gather information using multiple plug-in images
  oc adm must-gather --image=quay.io/kubevirt/must-gather --image=quay.io/openshift/origin-must-gather

  # Gather information using a specific image stream plug-in
  oc adm must-gather --image-stream=openshift/must-gather:latest

  # Gather information using a specific image, command, and pod-dir
  oc adm must-gather --image=my/image:tag --source-dir=/pod/directory -- myspecial-command.sh
oc adm new-project
Create a new project

Example usage

  # Create a new project using a node selector
  oc adm new-project myproject --node-selector='type=user-node,region=east'
oc adm node-logs
Display and filter node logs

Example usage

  # Show kubelet logs from all masters
  oc adm node-logs --role master -u kubelet

  # See what logs are available in masters in /var/logs
  oc adm node-logs --role master --path=/

  # Display cron log file from all masters
  oc adm node-logs --role master --path=cron
oc adm pod-network isolate-projects
Isolate project network

Example usage

  # Provide isolation for project p1
  oc adm pod-network isolate-projects <p1>

  # Allow all projects with label name=top-secret to have their own isolated project network
  oc adm pod-network isolate-projects --selector='name=top-secret'
oc adm pod-network join-projects
Join project network

Example usage

  # Allow project p2 to use project p1 network
  oc adm pod-network join-projects --to=<p1> <p2>

  # Allow all projects with label name=top-secret to use project p1 network
  oc adm pod-network join-projects --to=<p1> --selector='name=top-secret'
oc adm pod-network make-projects-global
Make project network global

Example usage

  # Allow project p1 to access all pods in the cluster and vice versa
  oc adm pod-network make-projects-global <p1>

  # Allow all projects with label name=share to access all pods in the cluster and vice versa
  oc adm pod-network make-projects-global --selector='name=share'
oc adm policy add-role-to-user
Add a role to users or service accounts for the current project

Example usage

  # Add the 'view' role to user1 for the current project
  oc adm policy add-role-to-user view user1

  # Add the 'edit' role to serviceaccount1 for the current project
  oc adm policy add-role-to-user edit -z serviceaccount1
oc adm policy add-scc-to-group
Add a security context constraint to groups

Example usage

  # Add the 'restricted' security context constraint to group1 and group2
  oc adm policy add-scc-to-group restricted group1 group2
oc adm policy add-scc-to-user
Add a security context constraint to users or a service account

Example usage

  # Add the 'restricted' security context constraint to user1 and user2
  oc adm policy add-scc-to-user restricted user1 user2

  # Add the 'privileged' security context constraint to serviceaccount1 in the current namespace
  oc adm policy add-scc-to-user privileged -z serviceaccount1
oc adm policy scc-review
Check which service account can create a pod

Example usage

  # Check whether service accounts sa1 and sa2 can admit a pod with a template pod spec specified in my_resource.yaml
  # Service Account specified in myresource.yaml file is ignored
  oc adm policy scc-review -z sa1,sa2 -f my_resource.yaml

  # Check whether service accounts system:serviceaccount:bob:default can admit a pod with a template pod spec specified in my_resource.yaml
  oc adm policy scc-review -z system:serviceaccount:bob:default -f my_resource.yaml

  # Check whether the service account specified in my_resource_with_sa.yaml can admit the pod
  oc adm policy scc-review -f my_resource_with_sa.yaml

  # Check whether the default service account can admit the pod; default is taken since no service account is defined in myresource_with_no_sa.yaml
  oc adm policy scc-review -f myresource_with_no_sa.yaml
oc adm policy scc-subject-review
Check whether a user or a service account can create a pod

Example usage

  # Check whether user bob can create a pod specified in myresource.yaml
  oc adm policy scc-subject-review -u bob -f myresource.yaml

  # Check whether user bob who belongs to projectAdmin group can create a pod specified in myresource.yaml
  oc adm policy scc-subject-review -u bob -g projectAdmin -f myresource.yaml

  # Check whether a service account specified in the pod template spec in myresourcewithsa.yaml can create the pod
  oc adm policy scc-subject-review -f myresourcewithsa.yaml
oc adm prune builds
Remove old completed and failed builds

Example usage

  # Dry run deleting older completed and failed builds and also including
  # all builds whose associated build config no longer exists
  oc adm prune builds --orphans

  # To actually perform the prune operation, the confirm flag must be appended
  oc adm prune builds --orphans --confirm
oc adm prune deployments
Remove old completed and failed deployment configs

Example usage

  # Dry run deleting all but the last complete deployment for every deployment config
  oc adm prune deployments --keep-complete=1

  # To actually perform the prune operation, the confirm flag must be appended
  oc adm prune deployments --keep-complete=1 --confirm
oc adm prune groups
Remove old OpenShift groups referencing missing records from an external provider

Example usage

  # Prune all orphaned groups
  oc adm prune groups --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Prune all orphaned groups except the ones from the blacklist file
  oc adm prune groups --blacklist=/path/to/blacklist.txt --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Prune all orphaned groups from a list of specific groups specified in a whitelist file
  oc adm prune groups --whitelist=/path/to/whitelist.txt --sync-config=/path/to/ldap-sync-config.yaml --confirm

  # Prune all orphaned groups from a list of specific groups specified in a whitelist
  oc adm prune groups groups/group_name groups/other_name --sync-config=/path/to/ldap-sync-config.yaml --confirm
oc adm prune images
Remove unreferenced images

Example usage

  # See what the prune command would delete if only images and their referrers were more than an hour old
  # and obsoleted by 3 newer revisions under the same tag were considered
  oc adm prune images --keep-tag-revisions=3 --keep-younger-than=60m

  # To actually perform the prune operation, the confirm flag must be appended
  oc adm prune images --keep-tag-revisions=3 --keep-younger-than=60m --confirm

  # See what the prune command would delete if we are interested in removing images
  # exceeding currently set limit ranges ('openshift.io/Image')
  oc adm prune images --prune-over-size-limit

  # To actually perform the prune operation, the confirm flag must be appended
  oc adm prune images --prune-over-size-limit --confirm

  # Force the insecure http protocol with the particular registry host name
  oc adm prune images --registry-url=http://registry.example.org --confirm

  # Force a secure connection with a custom certificate authority to the particular registry host name
  oc adm prune images --registry-url=registry.example.org --certificate-authority=/path/to/custom/ca.crt --confirm
oc adm release extract
Extract the contents of an update payload to disk

Example usage

  # Use git to check out the source code for the current cluster release to DIR
  oc adm release extract --git=DIR

  # Extract cloud credential requests for AWS
  oc adm release extract --credentials-requests --cloud=aws

  # Use git to check out the source code for the current cluster release to DIR from linux/s390x image
  # Note: Wildcard filter is not supported. Pass a single os/arch to extract
  oc adm release extract --git=DIR quay.io/openshift-release-dev/ocp-release:4.2.2 --filter-by-os=linux/s390x
oc adm release info
Display information about a release

Example usage

  # Show information about the cluster's current release
  oc adm release info

  # Show the source code that comprises a release
  oc adm release info 4.2.2 --commit-urls

  # Show the source code difference between two releases
  oc adm release info 4.2.0 4.2.2 --commits

  # Show where the images referenced by the release are located
  oc adm release info quay.io/openshift-release-dev/ocp-release:4.2.2 --pullspecs

  # Show information about linux/s390x image
  # Note: Wildcard filter is not supported. Pass a single os/arch to extract
  oc adm release info quay.io/openshift-release-dev/ocp-release:4.2.2 --filter-by-os=linux/s390x
oc adm release mirror
Mirror a release to a different image registry location

Example usage

  # Perform a dry run showing what would be mirrored, including the mirror objects
  oc adm release mirror 4.3.0 --to myregistry.local/openshift/release \
  --release-image-signature-to-dir /tmp/releases --dry-run

  # Mirror a release into the current directory
  oc adm release mirror 4.3.0 --to file://openshift/release \
  --release-image-signature-to-dir /tmp/releases

  # Mirror a release to another directory in the default location
  oc adm release mirror 4.3.0 --to-dir /tmp/releases

  # Upload a release from the current directory to another server
  oc adm release mirror --from file://openshift/release --to myregistry.com/openshift/release \
  --release-image-signature-to-dir /tmp/releases

  # Mirror the 4.3.0 release to repository registry.example.com and apply signatures to connected cluster
  oc adm release mirror --from=quay.io/openshift-release-dev/ocp-release:4.3.0-x86_64 \
  --to=registry.example.com/your/repository --apply-release-image-signature
oc adm release new
Create a new OpenShift release

Example usage

  # Create a release from the latest origin images and push to a DockerHub repo
  oc adm release new --from-image-stream=4.1 -n origin --to-image docker.io/mycompany/myrepo:latest

  # Create a new release with updated metadata from a previous release
  oc adm release new --from-release registry.svc.ci.openshift.org/origin/release:v4.1 --name 4.1.1 \
  --previous 4.1.0 --metadata ... --to-image docker.io/mycompany/myrepo:latest

  # Create a new release and override a single image
  oc adm release new --from-release registry.svc.ci.openshift.org/origin/release:v4.1 \
  cli=docker.io/mycompany/cli:latest --to-image docker.io/mycompany/myrepo:latest

  # Run a verification pass to ensure the release can be reproduced
  oc adm release new --from-release registry.svc.ci.openshift.org/origin/release:v4.1
oc adm taint
Update the taints on one or more nodes

Example usage

  # Update node 'foo' with a taint with key 'dedicated' and value 'special-user' and effect 'NoSchedule'
  # If a taint with that key and effect already exists, its value is replaced as specified
  oc adm taint nodes foo dedicated=special-user:NoSchedule

  # Remove from node 'foo' the taint with key 'dedicated' and effect 'NoSchedule' if one exists
  oc adm taint nodes foo dedicated:NoSchedule-

  # Remove from node 'foo' all the taints with key 'dedicated'
  oc adm taint nodes foo dedicated-

  # Add a taint with key 'dedicated' on nodes having label mylabel=X
  oc adm taint node -l myLabel=X  dedicated=foo:PreferNoSchedule

  # Add to node 'foo' a taint with key 'bar' and no value
  oc adm taint nodes foo bar:NoSchedule
oc adm top images
Show usage statistics for images

Example usage

  # Show usage statistics for images
  oc adm top images
oc adm top imagestreams
Show usage statistics for image streams

Example usage

  # Show usage statistics for image streams
  oc adm top imagestreams
oc adm top node
Display resource (CPU/memory) usage of nodes

Example usage

  # Show metrics for all nodes
  oc adm top node

  # Show metrics for a given node
  oc adm top node NODE_NAME
oc adm top pod
Display resource (CPU/memory) usage of pods

Example usage

  # Show metrics for all pods in the default namespace
  oc adm top pod

  # Show metrics for all pods in the given namespace
  oc adm top pod --namespace=NAMESPACE

  # Show metrics for a given pod and its containers
  oc adm top pod POD_NAME --containers

  # Show metrics for the pods defined by label name=myLabel
  oc adm top pod -l name=myLabel
oc adm uncordon
Mark node as schedulable

Example usage

  # Mark node "foo" as schedulable
  oc adm uncordon foo
oc adm upgrade
Upgrade a cluster or adjust the upgrade channel

Example usage

  # Review the available cluster updates
  oc adm upgrade

  # Update to the latest version
  oc adm upgrade --to-latest=true
oc adm verify-image-signature
Verify the image identity contained in the image signature

Example usage

  # Verify the image signature and identity using the local GPG keychain
  oc adm verify-image-signature sha256:c841e9b64e4579bd56c794bdd7c36e1c257110fd2404bebbb8b613e4935228c4 \
  --expected-identity=registry.local:5000/foo/bar:v1

  # Verify the image signature and identity using the local GPG keychain and save the status
  oc adm verify-image-signature sha256:c841e9b64e4579bd56c794bdd7c36e1c257110fd2404bebbb8b613e4935228c4 \
  --expected-identity=registry.local:5000/foo/bar:v1 --save

  # Verify the image signature and identity via exposed registry route
  oc adm verify-image-signature sha256:c841e9b64e4579bd56c794bdd7c36e1c257110fd2404bebbb8b613e4935228c4 \
  --expected-identity=registry.local:5000/foo/bar:v1 \
  --registry-url=docker-registry.foo.com

  # Remove all signature verifications from the image
  oc adm verify-image-signature sha256:c841e9b64e4579bd56c794bdd7c36e1c257110fd2404bebbb8b613e4935228c4 --remove-all
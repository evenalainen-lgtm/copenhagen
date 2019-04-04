# copenhagen
Jenkins-X Meetup

1. Sign-up for Oracle Cloud

2. Go to compute

	- Create oke.service user and add it to the administrators group
		Identity -> Users -> Create
		Navigate to the user and Create/Reset password, copy the password to clipboard
		Select Groups at bottom left, and add the user to Administrators Group
		Log out and log in again with the oke.service user
		
	- Create oke.policy to allow the Kubernetes PaaS service to manage the resources
		Identity -> Policies -> Create
		Create a new policy in the (root) compartment of your tenancy
		Keep policy current
		Policy statement: allow service OKE to manage all-resources in tenancy
		
	- Create oke.compartment for Oracle Kubernetes Engine
		Identity -> Compartments
		Create Compartment
		
	- Create OKE Cluster
		Developer Services -> Container Clusters (OKE)
		Create Cluster
		Optional - (Uncheck Tiller / Helm enabled)
		Leave other settings as is and create cluster
		
X. Create a jump box (optional)
	- Set up networking
		Networking -> Virtual Cloud Networks
		Create Virtual Cloud Network
		Select CREATE VIRTUAL CLOUD NETWORK PLUS RELATED RESOURCES
		Leave settings as is and Create Virtual Cloud Network
	
	- Create jump-box VM
		Compute -> Instances -> Create Instance
		Name your instance jump-box
		Paste you SSH key and leave other settings as is
		Once the VM has been created note the public IP address and log in via SSH: ssh opc@<vm.public.ip.address>
		Proceed to step 3.
		
3. Required Keys and OCID's and set up CLI

	- Create Keys and authorise your user
		https://docs.cloud.oracle.com/iaas/Content/API/Concepts/apisigningkey.htm
	
	- Set up CLI
		https://docs.cloud.oracle.com/iaas/Content/API/Concepts/cliconcepts.htm
		
	- oci setup config
	
4. Install Kubernetes tools and Git

	- Setup kubectl
		https://kubernetes.io/docs/tasks/tools/install-kubectl/
		
	- Setup helm (optional)
		https://helm.sh/docs/using_helm/
		
	- Setup Git
		https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
		https://git-scm.com/download/linux
		
	- Configure Kubectl
		Developer Services -> Container Clusters (OKE)
		Select cluster
		Access Kubeconfig
		
		
5. Install Jenkins-X

	- See also
		https://cloudnative.oracle.com/template.html#application-development/ci-cd/jenkinsx/tutorial.md
	
	- Install JX CLI and Jenkins-X system
		https://jenkins-x.io/getting-started/install/
	
	-Change Docker Registry to point to your OCIR Container Registry
		Create OCI auth token: User Settings -> Auth Tokens -> Generate Token and copy to clipboard
		Sign in to Jenkins Management console
		Manage Jenkins
		Find the DOCKER_REGISTRY variable and enter: iad.ocir.io/<name_of_your_OCI_tenant>
		Authorise Jenkins-X for OCIR: jx create docker auth --host "iad.ocir.io" /
										--user "<your_OCI_tenant>/<your_oci_user>" /
										--secret "<OCI_auth_token_just_created>" /
										--email "<your_email_address>"
										
6. Run Jenkins-X Quickstart

	- jx quickstart
	
7. Create a Kubernetes docker registry secret (see cloud native lab guide)
		https://cloudnative.oracle.com/template.html#application-development/ci-cd/jenkinsx/tutorial.md
		
	


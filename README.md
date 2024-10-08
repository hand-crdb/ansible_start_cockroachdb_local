# ansible_start_cockroachdb_local

[CockroachDB](https://www.cockroachlabs.com) docs show 
[how to start a 3-node local cluster using shell commands](https://www.cockroachlabs.com/docs/stable/start-a-local-cluster.html).  
Here are counterparts that do the same thing, but using 
[Ansible](https://en.wikipedia.org/wiki/Ansible_(software)).
Two Ansible playbooks are provided, to start CockroachDB in two modes:
* insecure
* secure

While these Ansible playbooks can speed creating your own local clusters, they are also simple examples of how to automate with Ansible, using an example that is well-known to people familiar with the docs.

**Notes**

These Ansible playbooks are idempotent, so you can run them multiple times safely:
* They check to see if the `cockroachdb` process is running for each of the 3 nodes before starting each node.  
* Similar logic applies to files and directories.
* The `cockroach init` command is always executed, but the error that will result from running it a second time is ignored.
* These playbooks differ from the documented commands in one respect: the `--store` parameter is modified so CockroachDB will not create a large 
[ballast file](https://www.cockroachlabs.com/docs/stable/cluster-setup-troubleshooting#automatic-ballast-files).

**Assumptions:**

* The `cockroach` command for the appropriate version of of CockroachDB should be in your search path.
* The working directory either is empty, or contains the store directories for the 3 nodes.  The store directories, if they exist, must have been created with a version of CockroachDB that is compatible with the version that you are starting.

## Insecure
ref: [Start a Local Cluster (Insecure)](https://www.cockroachlabs.com/docs/stable/start-a-local-cluster.html)

Example of how to execute:

```ansible-playbook ansible_cockroachdb_start_3_node_local_insecure.yaml```

## Secure

ref: [Start a Local Cluster (Secure)](https://www.cockroachlabs.com/docs/stable/secure-a-cluster.html)

Example of how to execute:

```ansible-playbook ansible_cockroachdb_start_3_node_local_secure.yaml```

**Assumptions:**

The working directory can either contain or not contain subdirectories for the certificates.  If these subdirectories already exist they will be used as-is.  If they do not exist, they will be created and populated with the certificate and private key files.

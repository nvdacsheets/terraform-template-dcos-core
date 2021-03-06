DC/OS Core Template
============
A Terraform module to install, upgrade, and modify nodes for DC/OS clusters in an automated fashion.

EXAMPLE - Bootstrap Node
-------

```hcl
module "dcos-bootstrap" {
   source  = "./modules/dcos-core"
   bootstrap_private_ip = "${aws_instance.bootstrap.private_ip}"
   dcos_install_mode = "${var.state}"
   dcos_version = "${var.dcos_version}"
   role = "dcos-bootstrap"
   dcos_bootstrap_port = "${var.custom_dcos_bootstrap_port}"
   custom_dcos_download_path = "${var.custom_dcos_download_path}"
   dcos_public_agent_list = "\n - ${join("\n - ", aws_instance.public-agent.*.private_ip)}"
   dcos_audit_logging = "${var.dcos_audit_logging}"
   dcos_auth_cookie_secure_flag = "${var.dcos_auth_cookie_secure_flag}"
   dcos_aws_access_key_id = "${var.dcos_aws_access_key_id}"
   dcos_aws_region = "${coalesce(var.dcos_aws_region, var.aws_region)}"
   dcos_aws_secret_access_key = "${var.dcos_aws_secret_access_key}"
   dcos_aws_template_storage_access_key_id = "${var.dcos_aws_template_storage_access_key_id}"
   dcos_aws_template_storage_bucket = "${var.dcos_aws_template_storage_bucket}"
   dcos_aws_template_storage_bucket_path = "${var.dcos_aws_template_storage_bucket_path}"
   dcos_aws_template_storage_region_name = "${var.dcos_aws_template_storage_region_name}"
   dcos_aws_template_storage_secret_access_key = "${var.dcos_aws_template_storage_secret_access_key}"
   dcos_aws_template_upload = "${var.dcos_aws_template_upload}"
   dcos_bouncer_expiration_auth_token_days = "${var.dcos_bouncer_expiration_auth_token_days}"
   dcos_adminrouter_tls_1_0_enabled = "${var.dcos_adminrouter_tls_1_0_enabled}"
   dcos_adminrouter_tls_1_1_enabled = "${var.dcos_adminrouter_tls_1_1_enabled}"
   dcos_adminrouter_tls_1_2_enabled = "${var.dcos_adminrouter_tls_1_2_enabled}"
   dcos_adminrouter_tls_cipher_suite= "${var.dcos_adminrouter_tls_cipher_suite}"
   dcos_ca_certificate_chain_path = "${var.dcos_ca_certificate_chain_path}"
   dcos_ca_certificate_key_path = "${var.dcos_ca_certificate_key_path}"
   dcos_ca_certificate_path = "${var.dcos_ca_certificate_path}"
   dcos_config= "${var.dcos_config}"
   dcos_custom_checks = "${var.dcos_custom_checks}"
   dcos_dns_bind_ip_blacklist = "${var.dcos_dns_bind_ip_blacklist}"
   dcos_enable_docker_gc= "${var.dcos_enable_docker_gc}"
   dcos_enable_gpu_isolation= "${var.dcos_enable_gpu_isolation}"
   dcos_fault_domain_detect_contents= "${var.dcos_fault_domain_detect_contents}"
   dcos_fault_domain_enabled= "${var.dcos_fault_domain_enabled}"
   dcos_gpus_are_scarce = "${var.dcos_gpus_are_scarce}"
   dcos_l4lb_enable_ipv6= "${var.dcos_l4lb_enable_ipv6}"
   dcos_license_key_contents= "${var.dcos_license_key_contents}"
   dcos_mesos_container_log_sink= "${var.dcos_mesos_container_log_sink}"
   dcos_mesos_dns_set_truncate_bit= "${var.dcos_mesos_dns_set_truncate_bit}"
   dcos_mesos_max_completed_tasks_per_framework = "${var.dcos_mesos_max_completed_tasks_per_framework}"
   dcos_ucr_default_bridge_subnet = "${var.dcos_ucr_default_bridge_subnet}"
   dcos_check_time = "${var.dcos_check_time}"
   dcos_cluster_docker_credentials = "${var.dcos_cluster_docker_credentials}"
   dcos_cluster_docker_credentials_dcos_owned = "${var.dcos_cluster_docker_credentials_dcos_owned}"
   dcos_cluster_docker_credentials_enabled = "${var.dcos_cluster_docker_credentials_enabled}"
   dcos_cluster_docker_credentials_write_to_etc = "${var.dcos_cluster_docker_credentials_write_to_etc}"
   dcos_cluster_name  = "${coalesce(var.dcos_cluster_name, data.template_file.cluster-name.rendered)}"
   dcos_customer_key = "${var.dcos_customer_key}"
   dcos_dns_search = "${var.dcos_dns_search}"
   dcos_dns_forward_zones = "${var.dcos_dns_forward_zones}"
   dcos_docker_remove_delay = "${var.dcos_docker_remove_delay}"
   dcos_exhibitor_address = "${aws_elb.internal-master-elb.dns_name}"
   dcos_exhibitor_azure_account_key = "${var.dcos_exhibitor_azure_account_key}"
   dcos_exhibitor_azure_account_name = "${var.dcos_exhibitor_azure_account_name}"
   dcos_exhibitor_azure_prefix = "${var.dcos_exhibitor_azure_prefix}"
   dcos_exhibitor_explicit_keys = "${var.dcos_exhibitor_explicit_keys}"
   dcos_exhibitor_storage_backend = "${var.dcos_exhibitor_storage_backend}"
   dcos_exhibitor_zk_hosts = "${var.dcos_exhibitor_zk_hosts}"
   dcos_exhibitor_zk_path = "${var.dcos_exhibitor_zk_path}"
   dcos_gc_delay = "${var.dcos_gc_delay}"
   dcos_http_proxy = "${var.dcos_http_proxy}"
   dcos_https_proxy = "${var.dcos_https_proxy}"
   dcos_log_directory = "${var.dcos_log_directory}"
   dcos_master_discovery = "${var.dcos_master_discovery}"
   dcos_master_dns_bindall = "${var.dcos_master_dns_bindall}"
   dcos_master_list = "\n - ${join("\n - ", aws_instance.master.*.private_ip)}"
   dcos_no_proxy = "${var.dcos_no_proxy}"
   dcos_num_masters = "${var.num_of_masters}"
   dcos_oauth_enabled = "${var.dcos_oauth_enabled}"
   dcos_overlay_config_attempts = "${var.dcos_overlay_config_attempts}"
   dcos_overlay_enable = "${var.dcos_overlay_enable}"
   dcos_overlay_mtu = "${var.dcos_overlay_mtu}"
   dcos_overlay_network = "${var.dcos_overlay_network}"
   dcos_process_timeout = "${var.dcos_process_timeout}"
   dcos_previous_version = "${var.dcos_previous_version}"
   dcos_agent_list = "\n - ${join("\n - ", aws_instance.agent.*.private_ip)}"
   dcos_resolvers  = "\n - ${join("\n - ", var.dcos_resolvers)}"
   dcos_rexray_config_filename = "${var.dcos_rexray_config_filename}"
   dcos_rexray_config_method = "${var.dcos_rexray_config_method}"
   dcos_s3_bucket = "${coalesce(var.dcos_s3_bucket, aws_s3_bucket.dcos_bucket.id)}"
   dcos_s3_prefix = "${coalesce(var.dcos_s3_prefix, aws_s3_bucket.dcos_bucket.id)}"
   dcos_security  = "${var.dcos_security}"
   dcos_superuser_password_hash = "${var.dcos_superuser_password_hash}"
   dcos_superuser_username = "${var.dcos_superuser_username}"
   dcos_telemetry_enabled = "${var.dcos_telemetry_enabled}"
   dcos_use_proxy = "${var.dcos_use_proxy}"
   dcos_zk_agent_credentials = "${var.dcos_zk_agent_credentials}"
   dcos_zk_master_credentials = "${var.dcos_zk_master_credentials}"
   dcos_zk_super_credentials = "${var.dcos_zk_super_credentials}"
   dcos_cluster_docker_registry_url = "${var.dcos_cluster_docker_registry_url}"
   dcos_rexray_config = "${var.dcos_rexray_config}"
   dcos_ip_detect_public_contents = "${var.dcos_ip_detect_public_contents}"
   dcos_ip_detect_contents = "${var.dcos_ip_detect_contents}"
   dcos_enable_docker_gc = "${var.dcos_enable_docker_gc}"
   dcos_staged_package_storage_uri = "${var.dcos_staged_package_storage_uri}"
   dcos_package_storage_uri = "${var.dcos_package_storage_uri}"
   dcos_enable_mesos_input_plugin = "${var.dcos_enable_mesos_input_plugin}"
}
resource "null_resource" "bootstrap" {
  triggers {
    cluster_instance_ids = "${aws_instance.bootstrap.id}"
    dcos_version = "${var.dcos_version}"
    dcos_security = "${var.dcos_security}"
    num_of_masters = "${var.num_of_masters}"
    dcos_audit_logging = "${var.dcos_audit_logging}"
    dcos_auth_cookie_secure_flag = "${var.dcos_auth_cookie_secure_flag}"
    dcos_aws_access_key_id = "${var.dcos_aws_access_key_id}"
    dcos_aws_region = "${coalesce(var.dcos_aws_region, var.aws_region)}"
    dcos_aws_secret_access_key = "${var.dcos_aws_secret_access_key}"
    dcos_aws_template_storage_access_key_id = "${var.dcos_aws_template_storage_access_key_id}"
    dcos_aws_template_storage_bucket = "${var.dcos_aws_template_storage_bucket}"
    dcos_aws_template_storage_bucket_path = "${var.dcos_aws_template_storage_bucket_path}"
    dcos_aws_template_storage_region_name = "${var.dcos_aws_template_storage_region_name}"
    dcos_aws_template_storage_secret_access_key = "${var.dcos_aws_template_storage_secret_access_key}"
    dcos_aws_template_upload = "${var.dcos_aws_template_upload}"
    dcos_bouncer_expiration_auth_token_days = "${var.dcos_bouncer_expiration_auth_token_days}"
    dcos_check_time = "${var.dcos_check_time}"
    dcos_cluster_docker_credentials = "${var.dcos_cluster_docker_credentials}"
    dcos_cluster_docker_credentials_dcos_owned = "${var.dcos_cluster_docker_credentials_dcos_owned}"
    dcos_cluster_docker_credentials_enabled = "${var.dcos_cluster_docker_credentials_enabled}"
    dcos_cluster_docker_credentials_write_to_etc = "${var.dcos_cluster_docker_credentials_write_to_etc}"
    dcos_customer_key = "${var.dcos_customer_key}"
    dcos_dns_search = "${var.dcos_dns_search}"
    dcos_dns_forward_zones = "${var.dcos_dns_forward_zones}"
    dcos_docker_remove_delay = "${var.dcos_docker_remove_delay}"
    dcos_exhibitor_address = "${aws_elb.internal-master-elb.dns_name}"
    dcos_exhibitor_azure_account_key = "${var.dcos_exhibitor_azure_account_key}"
    dcos_exhibitor_azure_account_name = "${var.dcos_exhibitor_azure_account_name}"
    dcos_exhibitor_azure_prefix = "${var.dcos_exhibitor_azure_prefix}"
    dcos_exhibitor_explicit_keys = "${var.dcos_exhibitor_explicit_keys}"
    dcos_exhibitor_storage_backend = "${var.dcos_exhibitor_storage_backend}"
    dcos_exhibitor_zk_hosts = "${var.dcos_exhibitor_zk_hosts}"
    dcos_exhibitor_zk_path = "${var.dcos_exhibitor_zk_path}"
    dcos_adminrouter_tls_1_0_enabled = "${var.dcos_adminrouter_tls_1_0_enabled}"
    dcos_adminrouter_tls_1_1_enabled = "${var.dcos_adminrouter_tls_1_1_enabled}"
    dcos_adminrouter_tls_1_2_enabled = "${var.dcos_adminrouter_tls_1_2_enabled}"
    dcos_adminrouter_tls_cipher_suite= "${var.dcos_adminrouter_tls_cipher_suite}"
    dcos_ca_certificate_chain_path = "${var.dcos_ca_certificate_chain_path}"
    dcos_ca_certificate_key_path = "${var.dcos_ca_certificate_key_path}"
    dcos_ca_certificate_path = "${var.dcos_ca_certificate_path}"
    dcos_config= "${var.dcos_config}"
    dcos_custom_checks = "${var.dcos_custom_checks}"
    dcos_cluster_name  = "${coalesce(var.dcos_cluster_name, data.template_file.cluster-name.rendered)}"
    dcos_dns_bind_ip_blacklist = "${var.dcos_dns_bind_ip_blacklist}"
    dcos_enable_docker_gc= "${var.dcos_enable_docker_gc}"
    dcos_enable_gpu_isolation= "${var.dcos_enable_gpu_isolation}"
    dcos_fault_domain_detect_contents= "${var.dcos_fault_domain_detect_contents}"
    dcos_fault_domain_enabled= "${var.dcos_fault_domain_enabled}"
    dcos_gpus_are_scarce = "${var.dcos_gpus_are_scarce}"
    dcos_l4lb_enable_ipv6= "${var.dcos_l4lb_enable_ipv6}"
    dcos_license_key_contents= "${var.dcos_license_key_contents}"
    dcos_mesos_container_log_sink= "${var.dcos_mesos_container_log_sink}"
    dcos_mesos_dns_set_truncate_bit= "${var.dcos_mesos_dns_set_truncate_bit}"
    dcos_mesos_max_completed_tasks_per_framework = "${var.dcos_mesos_max_completed_tasks_per_framework}"
    dcos_ucr_default_bridge_subnet = "${var.dcos_ucr_default_bridge_subnet}"
    dcos_gc_delay = "${var.dcos_gc_delay}"
    dcos_http_proxy = "${var.dcos_http_proxy}"
    dcos_https_proxy = "${var.dcos_https_proxy}"
    dcos_log_directory = "${var.dcos_log_directory}"
    dcos_master_discovery = "${var.dcos_master_discovery}"
    dcos_master_dns_bindall = "${var.dcos_master_dns_bindall}"
    dcos_no_proxy = "${var.dcos_no_proxy}"
    dcos_num_masters = "${var.num_of_masters}"
    dcos_oauth_enabled = "${var.dcos_oauth_enabled}"
    dcos_overlay_config_attempts = "${var.dcos_overlay_config_attempts}"
    dcos_overlay_enable = "${var.dcos_overlay_enable}"
    dcos_overlay_mtu = "${var.dcos_overlay_mtu}"
    dcos_overlay_network = "${var.dcos_overlay_network}"
    dcos_process_timeout = "${var.dcos_process_timeout}"
    dcos_previous_version = "${var.dcos_previous_version}"
    dcos_resolvers  = "\n - ${join("\n - ", var.dcos_resolvers)}"
    dcos_rexray_config_filename = "${var.dcos_rexray_config_filename}"
    dcos_rexray_config_method = "${var.dcos_rexray_config_method}"
    dcos_s3_bucket = "${coalesce(var.dcos_s3_bucket, aws_s3_bucket.dcos_bucket.id)}"
    dcos_s3_prefix = "${coalesce(var.dcos_s3_prefix, aws_s3_bucket.dcos_bucket.id)}"
    dcos_security  = "${var.dcos_security}"
    dcos_superuser_password_hash = "${var.dcos_superuser_password_hash}"
    dcos_superuser_username = "${var.dcos_superuser_username}"
    dcos_telemetry_enabled = "${var.dcos_telemetry_enabled}"
    dcos_use_proxy = "${var.dcos_use_proxy}"
    dcos_zk_agent_credentials = "${var.dcos_zk_agent_credentials}"
    dcos_zk_master_credentials = "${var.dcos_zk_master_credentials}"
    dcos_zk_super_credentials = "${var.dcos_zk_super_credentials}"
    dcos_cluster_docker_registry_url = "${var.dcos_cluster_docker_registry_url}"
    dcos_rexray_config = "${var.dcos_rexray_config}"
    dcos_ip_detect_public_contents = "${var.dcos_ip_detect_public_contents}"
    dcos_ip_detect_contents = "${var.dcos_ip_detect_contents}"
    dcos_enable_docker_gc = "${var.dcos_enable_docker_gc}"
    dcos_staged_package_storage_uri = "${var.dcos_staged_package_storage_uri}"
    dcos_package_storage_uri = "${var.dcos_package_storage_uri}"
    dcos_enable_mesos_input_plugin = "${var.dcos_enable_mesos_input_plugin}"
  }
  connection {
    host = "${element(aws_instance.bootstrap.*.public_ip, 0)}"
    user = "${module.aws-tested-oses.user}"
  }

  # Generate and upload bootstrap script to node
  provisioner "file" {
    content     = "${module.dcos-bootstrap.script}"
    destination = "run.sh"
  }

  # Install Bootstrap Script
  provisioner "remote-exec" {
    inline = [
      "sudo chmod +x run.sh",
      "sudo ./run.sh",
    ]
  }
}
```

EXAMPLE - Master Nodes
-------
Use this to make any type of Mesos agent you desire. In this example below is a public agent. You can have gpu agents, private agents, etc. They will be either use the `dcos-mesos-agent` or `dcos-mesos-agent-public` role.

```hcl

 # Create DCOS Mesos Master Scripts to execute
 module "dcos-mesos-master" {
   source               = "github.com/dcos/tf_dcos_core"
   bootstrap_private_ip = "${aws_instance.bootstrap.private_ip}"
   dcos_install_mode    = "${var.state}"
   dcos_version         = "${var.dcos_version}"
   dcos_skip_checks     = "${var.dcos_skip_checks}"
   role                 = "dcos-mesos-master"
 }

 resource "null_resource" "master" {
   triggers {
     cluster_instance_ids = "${null_resource.bootstrap.id}"
     current_ec2_instance_id = "${aws_instance.master.*.id[count.index]}"
   }
   connection {
     host = "${element(aws_instance.master.*.public_ip, count.index)}"
     user = "${module.aws-tested-oses.user}"
   }
   count = "${var.num_of_masters}"

   # Generate and upload Master script to node
   provisioner "file" {
     content     = "${module.dcos-mesos-master.script}"
     destination = "run.sh"
   }

   # Wait for bootstrapnode to be ready
   provisioner "remote-exec" {
     inline = [
      "until $(curl --output /dev/null --silent --head --fail http://${aws_instance.bootstrap.private_ip}/dcos_install.sh); do printf 'waiting for bootstrap node to serve...'; sleep 20; done"
     ]
   }

   # Install Master Script
   provisioner "remote-exec" {
     inline = [
       "sudo chmod +x run.sh",
       "sudo ./run.sh",
     ]
   }
 }
```

EXAMPLE - Agents
-------
```hcl
 module "dcos-mesos-agent-public" {
   source               = "github.com/dcos/tf_dcos_core"
   bootstrap_private_ip = "${aws_instance.bootstrap.private_ip}"
   dcos_install_mode    = "${var.state}"
   dcos_version         = "${var.dcos_version}"
   dcos_skip_checks     = "${var.dcos_skip_checks}"
   role                 = "dcos-mesos-agent-public"
 }

 # Execute generated script on agent
 resource "null_resource" "agent" {
   triggers {
     cluster_instance_ids = "${null_resource.bootstrap.id}"
     current_ec2_instance_id = "${aws_instance.agent.*.id[count.index]}"
   }
   connection {
     host = "${element(aws_instance.agent.*.public_ip, count.index)}"
     user = "${module.aws-tested-oses.user}"
   }
   count = "${var.num_of_private_agents}"

   # Generate and upload Agent script to node
   provisioner "file" {
     content     = "${module.dcos-mesos-agent.script}"
     destination = "run.sh"
   }

   # Wait for bootstrapnode to be ready
   provisioner "remote-exec" {
     inline = [
      "until $(curl --output /dev/null --silent --head --fail http://${aws_instance.bootstrap.private_ip}/dcos_install.sh); do printf 'waiting for bootstrap node to serve...'; sleep 20; done"
     ]
   }

   # Install Slave Node
   provisioner "remote-exec" {
     inline = [
       "sudo chmod +x run.sh",
       "sudo ./run.sh",
     ]
   }
 }
```


## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| bootstrap_private_ip | Private IP bootstrap nginx is listening on. Used to build the bootstrap URL. | string | `` | no |
| custom_dcos_download_path | insert location of dcos installer script (optional) | string | `` | no |
| dcos_adminrouter_tls_1_0_enabled | Indicates whether to enable TLSv1 support in Admin Router. (optional) | string | `` | no |
| dcos_adminrouter_tls_1_1_enabled | Indicates whether to enable TLSv1.1 support in Admin Router. (optional) | string | `` | no |
| dcos_adminrouter_tls_1_2_enabled | Indicates whether to enable TLSv1.2 support in Admin Router. (optional) | string | `` | no |
| dcos_adminrouter_tls_cipher_suite | [Enterprise DC/OS] Indicates whether to allow web browsers to send the DC/OS authentication cookie through a non-HTTPS connection. (optional) | string | `` | no |
| dcos_agent_list | used to list the agents in the config.yaml (optional) | string | `` | no |
| dcos_audit_logging | [Enterprise DC/OS] enable security decisions are logged for Mesos, Marathon, and Jobs. (optional) | string | `` | no |
| dcos_auth_cookie_secure_flag | [Enterprise DC/OS] allow web browsers to send the DC/OS authentication cookie through a non-HTTPS connection. (optional) | string | `` | no |
| dcos_aws_access_key_id | AWS key ID for exhibitor storage (optional but required with dcos_exhibitor_address) | string | `` | no |
| dcos_aws_region | AWS region for exhibitor storage (optional but required with dcos_exhibitor_address) | string | `` | no |
| dcos_aws_secret_access_key | AWS secret key for exhibitor storage (optional but required with dcos_exhibitor_address) | string | `` | no |
| dcos_aws_template_storage_access_key_id | AWS key ID for CloudFormation template storage (optional) | string | `` | no |
| dcos_aws_template_storage_bucket | AWS CloudFormation bucket name (optional) | string | `` | no |
| dcos_aws_template_storage_bucket_path | AWS CloudFormation bucket path (optional) | string | `` | no |
| dcos_aws_template_storage_region_name | AWS CloudFormation region name (optional) | string | `` | no |
| dcos_aws_template_storage_secret_access_key | AWS secret key for the CloudFormation template (optional) | string | `` | no |
| dcos_aws_template_upload | To automatically upload the customized advanced templates to your S3 bucket. (optional) | string | `` | no |
| dcos_bootstrap_port | Port of the bootstrap URL | string | `80` | no |
| dcos_bouncer_expiration_auth_token_days | [Enterprise DC/OS] Sets the auth token time-to-live (TTL) for Identity and Access Management. (optional) | string | `` | no |
| dcos_ca_certificate_chain_path | [Enterprise DC/OS] Path (relative to the $DCOS_INSTALL_DIR) to a file containing the complete CA certification chain required for end-entity certificate verification, in the OpenSSL PEM format. (optional) | string | `` | no |
| dcos_ca_certificate_key_path | DC/OS CA certificate key path | string | `` | no |
| dcos_ca_certificate_path | [Enterprise DC/OS] Path (relative to the $DCOS_INSTALL_DIR) to a file containing a single X.509 CA certificate in the OpenSSL PEM format. (optional) | string | `` | no |
| dcos_check_time | Check if Network Time Protocol (NTP) is enabled during DC/OS startup. (optional) | string | `` | no |
| dcos_cluster_docker_credentials | Dictionary of Docker credentials to pass. (optional) | string | `` | no |
| dcos_cluster_docker_credentials_dcos_owned | Indicates whether to store the credentials file in /opt/mesosphere or /etc/mesosphere/docker_credentials. A sysadmin cannot edit /opt/mesosphere directly (optional) | string | `` | no |
| dcos_cluster_docker_credentials_enabled | Indicates whether to pass the Mesos --docker_config option to Mesos. (optional) | string | `` | no |
| dcos_cluster_docker_credentials_write_to_etc | Indicates whether to write a cluster credentials file. (optional) | string | `` | no |
| dcos_cluster_docker_registry_enabled | DC/OS cluster docker registry enabled | string | `` | no |
| dcos_cluster_docker_registry_url | The custom URL that Mesos uses to pull Docker images from. If set, it will configure the Mesos --docker_registry flag to the specified URL. (optional) | string | `` | no |
| dcos_cluster_name | sets the DC/OS cluster name | string | `` | no |
| dcos_config | used to add any extra arguments in the config.yaml that are not specified here. (optional) | string | `` | no |
| dcos_custom_checks | Custom installation checks that are added to the default check configuration process. (optional) | string | `` | no |
| dcos_customer_key | [Enterprise DC/OS] sets the customer key (optional) | string | `` | no |
| dcos_dns_bind_ip_blacklist | A list of IP addresses that DC/OS DNS resolvers cannot bind to. (optional) | string | `` | no |
| dcos_dns_forward_zones | Allow to forward DNS to certain domain requests to specific server. The following syntax must be used in combination with Terraform string heredoc. (optional) (:warning: DC/OS 1.10+) | string | `` | no |
| dcos_dns_search | A space-separated list of domains that are tried when an unqualified domain is entered. (optional) | string | `` | no |
| dcos_docker_remove_delay | The amount of time to wait before removing stale Docker images stored on the agent nodes and the Docker image generated by the installer. (optional) | string | `` | no |
| dcos_enable_docker_gc | Indicates whether to run the docker-gc script, a simple Docker container and image garbage collection script, once every hour to clean up stray Docker containers. (optional) | string | `` | no |
| dcos_enable_gpu_isolation | Indicates whether to enable GPU support in DC/OS. (optional) | string | `` | no |
| dcos_enable_mesos_input_plugin | Indicates whether to enable Telegraf's Mesos input plugin to collect Mesos metrics from Mesos masters and agents. Options: `true` or `false` (optional) | string | `` | no |
| dcos_exhibitor_address | The address of the load balancer in front of the masters (recommended) | string | `` | no |
| dcos_exhibitor_azure_account_key | the azure account key for exhibitor storage (optional but required with dcos_exhibitor_address) | string | `` | no |
| dcos_exhibitor_azure_account_name | the azure account name for exhibitor storage (optional but required with dcos_exhibitor_address) | string | `` | no |
| dcos_exhibitor_azure_prefix | the azure account name for exhibitor storage (optional but required with dcos_exhibitor_address) | string | `` | no |
| dcos_exhibitor_explicit_keys | set whether you are using AWS API keys to grant Exhibitor access to S3. (optional) | string | `` | no |
| dcos_exhibitor_storage_backend | options are static, aws_s3, azure, or zookeeper (recommended) | string | `` | no |
| dcos_exhibitor_zk_hosts | a comma-separated list of one or more ZooKeeper node IP and port addresses to use for configuring the internal Exhibitor instances. (not recommended but required with exhibitor_storage_backend set to ZooKeeper. Use aws_s3 or azure instead. Assumes external ZooKeeper is already online.) | string | `` | no |
| dcos_exhibitor_zk_path | the filepath that Exhibitor uses to store data (not recommended but required with exhibitor_storage_backend set to zookeeper. Use aws_s3 or azureinstead. Assumes external ZooKeeper is already online.) | string | `` | no |
| dcos_fault_domain_detect_contents | [Enterprise DC/OS] fault domain script contents. Optional but required if no fault-domain-detect script present. | string | `` | no |
| dcos_fault_domain_enabled | [Enterprise DC/OS] used to control if fault domain is enabled | string | `` | no |
| dcos_gc_delay | The maximum amount of time to wait before cleaning up the executor directories (optional) | string | `` | no |
| dcos_gpus_are_scarce | Indicates whether to treat GPUs as a scarce resource in the cluster. (optional) | string | `` | no |
| dcos_http_proxy | http proxy (optional) | string | `` | no |
| dcos_https_proxy | https proxy (optional) | string | `` | no |
| dcos_install_mode | Type of command to execute. Options: install or upgrade | string | `install` | no |
| dcos_ip_detect_contents | Allows DC/OS to detect your private address. Use this to pass this as an input to the module rather than a file in side your bootstrap node. (recommended) | string | `` | no |
| dcos_ip_detect_public_contents | Allows DC/OS to be aware of your publicly routeable address for ease of use (recommended) | string | `` | no |
| dcos_ip_detect_public_filename | statically set your detect-ip-public path | string | `` | no |
| dcos_l4lb_enable_ipv6 | A boolean that indicates if layer 4 load balancing is available for IPv6 networks. (optional) | string | `` | no |
| dcos_license_key_contents | [Enterprise DC/OS] used to privide the license key of DC/OS for Enterprise Edition. Optional if license.txt is present on bootstrap node. | string | `` | no |
| dcos_log_directory | The path to the installer host logs from the SSH processes. (optional) | string | `` | no |
| dcos_master_discovery | The Mesos master discovery method. The available options are static or master_http_loadbalancer. (recommend the use of master_http_loadbalancer) | string | `` | no |
| dcos_master_dns_bindall | Indicates whether the master DNS port is open. (optional) | string | `` | no |
| dcos_master_external_loadbalancer | Allows DC/OS to configure certs around the External Load Balancer name. If not used SSL verfication issues will arrise. EE only. (recommended) | string | `` | no |
| dcos_master_list | statically set your master nodes (not recommended but required with exhibitor_storage_backend set to static. Use aws_s3 or azure instead, that way you can replace masters in the cloud.) | string | `` | no |
| dcos_mesos_container_log_sink | The log manager for containers (tasks). The options are to send logs to: 'journald', 'logrotate', 'journald+logrotate'. (optional) | string | `` | no |
| dcos_mesos_dns_set_truncate_bit | Indicates whether to set the truncate bit if the response is too large to fit in a single packet. (optional) | string | `` | no |
| dcos_mesos_max_completed_tasks_per_framework | The number of completed tasks for each framework that the Mesos master will retain in memory. (optional) | string | `` | no |
| dcos_no_proxy | A YAML nested list (-) of addresses to exclude from the proxy. (optional) | string | `` | no |
| dcos_num_masters | set the num of master nodes (required with exhibitor_storage_backend set to aws_s3, azure, ZooKeeper) | string | `` | no |
| dcos_oauth_enabled | [Open DC/OS Only] Indicates whether to enable authentication for your cluster. (optional) | string | `` | no |
| dcos_overlay_config_attempts | Specifies how many failed configuration attempts are allowed before the overlay configuration modules stop trying to configure an virtual network. (optional) | string | `` | no |
| dcos_overlay_enable | Enable to disable overlay (optional) | string | `` | no |
| dcos_overlay_mtu | The maximum transmission unit (MTU) of the Virtual Ethernet (vEth) on the containers that are launched on the overlay. (optional) | string | `` | no |
| dcos_overlay_network | This group of parameters define an virtual network for DC/OS. (optional) | string | `` | no |
| dcos_package_storage_uri | Where to permanently store DC/OS packages. The value must be a file URL. (optional) | string | `` | no |
| dcos_previous_version | DC/OS 1.9+ requires users to set this value to ensure users know the version. Terraform helps populate this value, but users can override it here. (recommended) | string | `` | no |
| dcos_previous_version_master_index | Used to track the index of master for quering the previous DC/OS version during upgrading. (optional) applicable: 1.9+ | string | `0` | no |
| dcos_process_timeout | The allowable amount of time, in seconds, for an action to begin after the process forks. (optional) | string | `` | no |
| dcos_public_agent_list | statically set your public agents (not recommended) | string | `` | no |
| dcos_resolvers | A YAML nested list (-) of DNS resolvers for your DC/OS cluster nodes. (recommended) | string | `` | no |
| dcos_rexray_config | The REX-Ray configuration method for enabling external persistent volumes in Marathon. (optional) | string | `` | no |
| dcos_rexray_config_filename | The REX-Ray configuration filename for enabling external persistent volumes in Marathon. (optional) | string | `` | no |
| dcos_rexray_config_method | The REX-Ray configuration method for enabling external persistent volumes in Marathon. (optional) | string | `` | no |
| dcos_s3_bucket | name of the s3 bucket for the exhibitor backend (recommended but required with dcos_exhibitor_address) | string | `` | no |
| dcos_s3_prefix | name of the s3 prefix for the exhibitor backend (recommended but required with dcos_exhibitor_address) | string | `` | no |
| dcos_security | [Enterprise DC/OS] set the security level of DC/OS, either 'strict' or 'permissive'. Default is 'permissive'. (recommended) | string | `` | no |
| dcos_skip_checks | Upgrade option: Used to skip all dcos checks that may block an upgrade if any DC/OS component is unhealthly. (optional) applicable: 1.10+ | string | `true` | no |
| dcos_staged_package_storage_uri | Where to temporarily store DC/OS packages while they are being added. (optional) | string | `` | no |
| dcos_superuser_password_hash | [Enterprise DC/OS] set the superuser password hash (recommended) | string | `` | no |
| dcos_superuser_username | [Enterprise DC/OS] set the superuser username (recommended) | string | `` | no |
| dcos_telemetry_enabled | Change the telemetry option (optional) | string | `` | no |
| dcos_ucr_default_bridge_subnet | IPv4 subnet allocated to the mesos-bridge CNI network for UCR bridge-mode networking. (optional) | string | `` | no |
| dcos_use_proxy | To enable use of proxy for internal routing (optional) | string | `` | no |
| dcos_variant | Main Variables | string | `open` | no |
| dcos_version | Specifies which DC/OS version instruction to use. Options: 1.9.0, 1.8.8, etc. See dcos_download_path or dcos_version tree for a full list. | string | `1.9.0` | no |
| dcos_zk_agent_credentials | [Enterprise DC/OS] set the ZooKeeper agent credentials (recommended) | string | `` | no |
| dcos_zk_master_credentials | [Enterprise DC/OS] set the ZooKeeper master credentials (recommended) | string | `` | no |
| dcos_zk_super_credentials | [Enterprise DC/OS] set the zk super credentials (recommended) | string | `` | no |
| role | specifies which dcos role of commands to run. Options: `dcos-bootstrap`, `dcos-mesos-agent-public`, `dcos-mesos-agent` and `dcos-mesos-master` | string | - | yes |

## Outputs

| Name | Description |
|------|-------------|
| script | The battle-tested provisioner contents of the output by DC/OS role to perform requried admin actions in behalf of the user as documented in http://mesosphere.com and http://dcos.io |


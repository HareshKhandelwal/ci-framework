# Available hooks description

## ceph-deploy.yml
This hook allow to deploy the "toy ceph" as explained [here](https://github.com/fultonj/zed/tree/main/edpm).
### Output
* `cifmw_ceph_conf`: secret generated by the ceph installation, to be used for
consumers (base64 encoded).
* `cifmw_ceph_fsid`: ceph FSID generated by the ceph installation.

## kustomize_cr.yml
This hook enables customization of CR files, using oc kustomize.
### Input
* `cifmw_kustomize_cr_artifact_dir`: (Optional) Destination directory to place the
generated kustomized CR file. Defaults to "*{{ ansible_user_dir }}/ci-framework-data/kustomize_cr*".
* `cifmw_kustomize_cr_include_vars`: (Optional) List of files to be loaded
before running kustomize.
* `cifmw_kustomize_cr_file_path`: Path to directory containing the CR file.
* `cifmw_kustomize_cr_file_name`: File name of the CR file to be kustomized.
* `cifmw_kustomize_cr_template`: Relative path to kustomization template file.
This path should be relative to hook playbook directory.
### Output
* `kustomized_{{ cifmw_kustomize_cr_file_name }}`: Kustomized file which is
available at *cifmw_kustomize_cr_artifact_dir* to be consumed by the deployment.

## kuttl_openstack_prep.yml
This hook provides openstack_prep variables for kuttl tests.
### Input
None
### Output
* `cifmw_kuttl_openstack_prep_vars`: Environment variable to be used during openstack_prep
step in install_yamls.

## noop.yml
Just a dummy hook, mostly used as a demonstrator of the hook workflow.

It doesn't have any output.

## rabbitmq_tuning.yml
Tunes rabbitmq with more conservative resources. Useful for small environment,
such as CI.

It doesn't have any output.

## restart_nova_scheduler.yml
Restarts nova-scheduler in order to refresh known cells. Useful in CI, mostly,
but may be used elsewhere in case you want to add compute/cells.

It doesn't have any output.

## validate_podified_deployment.yml
Ensure podified deployment is successful by checking the running pods/services.

It doesn't have any output.

## link2file.yml

This play replaces the given soft links with their respective source files. It
is required to avoid kustomize errors when using symbolic links. This play has
no output.

### Required variables - link2file

* `cifmw_link2file_files` (str) A comma separated string of file names to be
  replaced.
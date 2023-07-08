# lab_provision

## Description

**lab_provision** is an Ansible project that provisions and configures virtual machines on RHEL-like hosts using the KVM hyperviser.

This project is heavily enspired from the [Build a lab in 36 seconds with Ansible](https://www.redhat.com/sysadmin/build-VM-fast-ansible) article by _Ricardo Gerardi_ which is based on the [Build a lab in five minutes with three simple commands](https://www.redhat.com/sysadmin/build-lab-quickly) article from Alex Callejas; Reading these projects is recommended to see the evolution tof the concept.

## Project Structure

This project is divided to two main parts, which are in turn represented in the 2 Ansible roles

- **kvm_provision**
- **host_configure**

---

### kvm_provision

This role provisions the guest vms defined in the variable `vm_list` and ensures the most basic guest connectivity steps.

**Role features:**

- Provision vm guests
- Adds provisioned vms hostnames to host's `/etc/hosts` file
- Update `known_hosts` file (to avoid ssh key fingerprint connection errors)

**Role variables:**

- `iventory/vm_hosts/vars/vm_guests/*`
- `roles/kvm_provision/defaults/main.yml`

---

### host_configure

This role performs post-provisioning configuration in vm guests. Please note that most of these steps can be disabled via boolean variables.

**Role features:**

- **Basic configuration:**
  - send host's ssh key
  - set keyboard layout
  - send host's `/etc/hosts` file
  - configure host's command alias in guests
- **Package configuration:**
  - configure dnf
  - configure redhat subscription if provisioned guests are running RHEL
  - install packages defined in the `packages` variable
  - Update host
  - Clean obsolete packages
  - Remove RHEL subscription

**Role variables:**

- `iventory/vm_guests/vars/vm_guests/vars`
- `roles/host_configure/defaults/main.yml`

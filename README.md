# Abaqus in Apptainer/Singularity container
The Apptainer/Singularity containerization technology streamlines the containerization process of Abaqus with OpenMPI and Intel OneAPI compilers, ensuring compatibility with (almost) any Linux distribution., enhances portability and enables a seamless deployment of Abaqus across existing computing environments. The provided Definition file assumes CentOS 7 as the base OS, but it can be used on other distributions as well. If you encounter any issues due to differences between other distributions and CentOS 7, you may need to adjust the Definition file accordingly. Additionally, ensure that the necessary dependencies and packages are available on the host system.

To install Apptainer on CentOS 7 you can use EPEL repository:
```
~]$ sudo yum -y install epel-release
~]$ sudo yum install apptainer apptainer-suid
```
Put the following files required for installation into directory ~/2024:
* [2024.AM_SIM_Abaqus_Extend.AllOS.1-6.tar](https://software.3ds.com/)
* [2024.AM_SIM_Abaqus_Extend.AllOS.2-6.tar](https://software.3ds.com/)
* [2024.AM_SIM_Abaqus_Extend.AllOS.3-6.tar](https://software.3ds.com/)
* [2024.AM_SIM_Abaqus_Extend.AllOS.4-6.tar](https://software.3ds.com/)
* [2024.AM_SIM_Abaqus_Extend.AllOS.5-6.tar](https://software.3ds.com/)
* [2024.AM_SIM_Abaqus_Extend.AllOS.6-6.tar](https://software.3ds.com/)
* [UserIntentions_CODE.xml](https://help.3ds.com/2024/english/dssimulia_established/estiinstallmap/esti-t-autosilentinstallersuite.htm?contextscope=all)
* [UserIntentions_CAA_Additional_426.xml](https://help.3ds.com/2024/english/dssimulia_established/estiinstallmap/esti-t-autosilentinstallersuite.htm?contextscope=all)
* [openmpi-4.0.5-3.el8.x86_64.rpm](https://centos.pkgs.org/8-stream/centos-appstream-x86_64/openmpi-4.0.5-3.el8.x86_64.rpm.html)
* [openmpi-devel-4.0.5-3.el8.x86_64.rpm](https://centos.pkgs.org/8-stream/centos-appstream-x86_64/openmpi-devel-4.0.5-3.el8.x86_64.rpm.html)
* [libfabric-1.11.2-1.el8.x86_64.rpm](https://centos.pkgs.org/8-stream/centos-baseos-x86_64/libfabric-1.11.2-1.el8.x86_64.rpm.html)
* [oneAPI.repo](2024/oneAPI.repo)
* [lic.conf](2024/lic.conf)

Use the following commands to build the Apptainer/Singularity container:
```
~]$ sudo apptainer build abaqus-2024.sif abaqus-2024-EL7.def
```
Please note that the Apptainer container with Abaqus can be run and built in rootless mode as well. Please follow the [Apptainer documentation](https://apptainer.org/docs/admin/main/user_namespace.html) to allow an unprivileged user to build and run a container with Abaqus.

To run Abaqus 2024 in the container execute the command:
```
~]$ apptainer exec abaqus-2024.sif abaqus -info ver
```
or start an interactive shell within the container to run Abaqus commands as needed:
```
~]$ apptainer shell abaqus-2024.sif
Apptainer> . /opt/intel/oneapi/compiler/latest/env/vars.sh
Apptainer> abq2024 verify all
```

Happy using Abaqus in the Apptainer/Singularity container on Linux.

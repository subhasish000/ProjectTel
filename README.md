Design Document
## Table of contents

- [Steps to use the script](#steps-to-use-the-script)
- [Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)
- [Build](#build)
    - [Install and Configure NNMi](#install-and-configure-nnmi)
    - [Install and Configure OA](#install-and-configure-oa)
- [Rebuild](#rebuild)
    - [Uninstall OA and NNMi](#uninstall-oa-and-nnmi)
    - [Install and Configure NNMi](#install-and-configure-nnmi)
    - [Install and Configure OA](#install-and-configure-oa)
- [Testing for RPOP lite build](#testing-for-rpop-lite-build)
- [All](#all)
    - [Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)
    - [Build](#build)
    - [Testing for RPOP lite build](#testing-for-rpop-lite-build)
- [Appendix](#appendix)
    - [Uninstall OA and NNMi **666** option](#uninstall-oa-and-nnmi-666-option)

## Steps to use the script

- Login to the ansible server.

- Download the scripts ( ansible_frame_main.s & rpop_lite.sh ) from the below link to **"/ansible/RPOP_lite"**.

      https://git.in.telstra.com.au/WIAN/USMOpsBridge/tree/Development/RPOP_lite/ansible-rpop-lite/framework_scripts
      
- Execute the below command to provide full permission to the script.
            
         chmod 777 ansible_frame_main.sh

**Note**:

+ Make sure **ansible-rpop-lite** folder is present under **/ansible/RPOP_lite/**, if not, create a folder RPOP under /ansible and download the **ansible-rpop-lite** folder from the below link to **/ansible/RPOP_lite**.

     https://git.in.telstra.com.au/WIAN/USMOpsBridge/tree/Development/RPOP_lite
     
+ Also make sure **installers** folder is present under **/ansible/RPOP/ansible-rpop/**, if not download the **installers** folder from the below link to **/ansible/RPOP/ansible-rpop/**

    https://git.in.telstra.com.au/WIAN/USMOpsBridge/tree/Development/ansible-rpop

# Pre-requisites for RPOP lite build

**Note:** 

Make sure to remove RPOP lite server details from the **/etc/ansible/hosts** file.

- Navigate to **/ansible/RPOP_lite** path and execute the script as shown below.

            ./ansible_main_frame.sh

- Select option **3** for RPOP lite build.

![alt text](docs/rpopenv.PNG "RPOP lite option")

- Select option **1** to perform the Pre-requisites check.

![alt text](docs/precheckop.PNG "Precheck option")

- Enter the server details and credentials for the RPOP server.

![alt text](docs/prereqin.PNG "Precheck input option")

During the pre-requirements check, if any of the pre-requisite are not met, the script installs the particular package.

- The RPOP lite server details are updated in **/etc/ansible/hosts** of Ansible server.

- The RPOP lite server details are updated in **/etc/hosts** of the respective server.

- Once the details are successfully updated, the PLAY RECAP section will be displayed with **failed=0**, which indicates the successful completion of the task.

![alt text](docs/rpop_itehostupdate.PNG "host update")

- Press Enter to check the RPOP pre-requisites in both the RPOP servers. The output will be similar to the below screenshot.

![alt text](docs/prere.PNG "Prereq")

![alt text](docs/prere1.PNG "Prereq")

- Press Enter to check NNMi and OA prechecks. If any of the pre-requisites is missing, it will install the package automatically.

- During the execution of each task, if the output contains **ok**, it indicates no changes has been done. If the output contains **changed**, it indicates an update has been done.

- Each colour specified in the output indicates as below:
      - Green -> Success and no changes done
      - Yellow -> Success and changes are done
      - Red -> Error (which can be ignored if it is showing ignoring)
      - Purple -> Warnings which can be ignored
      - Blue -> Skipping which can be ignored

- After successful completion of pre-requisites, the script prompts to choose the type of installation.

[Back to Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)

# Build

- Select option **2** to proceed with RPOP lite build.

![alt text](docs/buildin.PNG "Build option")

- Enter the RPOP lite server FQDN and IP as below.

![alt text](docs/buildinpu.PNG "Build option")

- A summary of user input is displayed. Type 'y' to proceed with the build.

- The RPOP lite server details are updated in **/etc/ansible/hosts** of Ansible server.

- The RPOP lite server details are updated in **/etc/hosts** of the respective server.

- Press Enter to proceed with NNMi installation for RPOP lite server. 

### Install and Configure NNMi

- If NNMi is already installed, the installation is skipped. NNMi version is checked, to verify if NNMi is installed. If NNMi is not installed, the version check shows an error, which can be ignored.

![alt text](docs/nnmvers.PNG "NNMi_version")

- After the successful completion of NNMi version check, it will proceed with NNMi installation. The below error in NNMi installation can be ignored, as it tries to install again, in case the installation fails.

![alt text](docs/rpop_lite_nnminstall.PNG "NNMi installation")

![alt text](docs/rpop_lite_nnm.PNG "NNMi installation")

- Press Enter to install NNMi patch on RPOP lite server.

- Press Enter to proceed with the NNMi configuration. It includes the below tasks:

    - Disable Trap receiver
    - Configure Status Polling
    - Configure Node Down Event
    - Disable All the Remaining Correlations
    - NNMi backup
    - NNM Data Warehousing
    - NNMi user creation

### Install and Configure OA

- If OA is already installed, the installation is skipped. OA version is checked, to verify if OA is installed. The version check shows an error, if OA is not installed. This can be ignored.

![alt text](docs/OAversioncheckforinstall.PNG "OA check")

- Once the OA version check is completed, press Enter to proceed with the OA installation on RPOP lite server.

![alt text](docs/rpoplite_oains.PNG "OA installlation")

![alt text](docs/oains1.PNG "OA installlation")

![alt text](docs/oains2.PNG "OA installlation")

- Once OA is installed without any errors, it proceeds with OA post installation.

![alt text](docs/rpop_lte_oapost.PNG "OA post install")

- After the successful completion of build, the script will prompt to choose the type of installation.

[Back to Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)

# Rebuild

- Rebuild option allows the user to rebuild (uninstall/install) NNMi and OA.

- Select option **3** to rebuild the RPOP lite server.

![alt text](docs/rebuildin.PNG "rebuild_option")

- It will prompt to Enter the username and password for RPOP lite server.

- A summary of user input is displayed. Type 'y' to proceed with the build.

- The RPOP lite server details are updated in **/etc/ansible/hosts** of Ansible server.

- The RPOP lite server details are updated in **/etc/hosts** of the respective server.

### Uninstall OA and NNMi

- Press Enter to check whether OA is installed. If installed, it will uninstall or else it will skip the uninstallation. 

![alt text](docs/oaver.PNG "oa_version")

- Press Enter to proceed with OA uninstallation.

![alt text](docs/rpop_liteoauninstall.PNG "OA uninstallation")

- After successful uninstallation of OA, press Enter to continue with NNMi version check.

![alt text](docs/rpoplitennmunins.PNG "NNMi_version")

- If NNMi is installed, then it would be uninstalled, "check if agent is installed" and "Fail message" tasks shows an error if the agent is not installed, which can be ignored.

![alt text](docs/nnmunins.PNG "NNMi_uninstall")

![alt text](docs/nnmuninst1.PNG "NNMi_uninstall")

![alt text](docs/nnmuninst2.PNG "NNMi_uninstall")

### Install and Configure NNMi 

- Once all application uninstallation is done, press Enter to begin RPOP Build. Firstly, it checks the RPOP pre-requsiites and then proceeds with NNMi installation.

- If NNMi is already installed, the installation is skipped. NNMi version is checked, to verify if NNMi is installed. If NNMi is not installed, the version check shows an error, which can be ignored.

![alt text](docs/nnmvers.PNG "nnm version check")

- After the successful completion of NNMi version check, it will proceed with NNMi installation. The below error in NNMi installation can be ignored, as it tries to install again, in case the installation fails.

![alt text](docs/rpop_lite_nnminstall.PNG "NNMi installation")

![alt text](docs/rpop_lite_nnm.PNG "NNMi installation")

- Press Enter to install NNMi patch on RPOP lite server.

- Press Enter to proceed with the NNMi configuration. It includes the below tasks:

    - Disable Trap receiver
    - Configure Status Polling
    - Configure Node Down Event
    - Disable All the Remaining Correlations
    - NNMi backup
    - NNM Data Warehousing
    - NNMi user creation

### Install and Configure OA 

- If OA is already installed, the installation is skipped. OA version is checked, to verify if OA is installed. The version check shows an error, if OA is not installed. This can be ignored.

![alt text](docs/OAversioncheckforinstall.PNG "OA check")

- Once the OA version check is completed, press Enter to proceed with the OA installation on RPOP lite server.

![alt text](docs/rpoplite_oains.PNG "OA installlation")

![alt text](docs/oains1.PNG "OA installlation")

![alt text](docs/oains2.PNG "OA installlation")

- Once OA is installed without any errors, it proceeds with OA post installation.

![alt text](docs/rpop_lte_oapost.PNG "OA post install")

- After the successful completion of build, the script will prompt to choose the type of installation.

[Back to Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)

# Testing for RPOP build

- Select option **4** to perform the RPOP lite functionality testing.

![alt text](docs/testingin.PNG "Teting option")

- Provide the server details and password when prompted.

![alt text](docs/buildinpu.PNG "Teting input")

- The host file is updated with the RPOP details in the Ansible server. The primary and secondary server details will also be updated in /etc/hosts file of the respective RPOP servers. Once the details are successfully updated, the PLAY RECAP section will be displayed with **failed=0**, indicating the successful completion of the task.

![alt text](docs/rpop_itehostupdate.PNG "host update")

- Press Enter to create test reports in RPOP lite server.

![alt text](docs/testre.PNG "Test report")

- Press Enter to run the test case to verify IP and hostname in RPOP lite server.

![alt text](docs/iphostcheck.PNG "IP and Host check")

- Press Enter to run the test case to verify if the host file is updated in RPOP lite server.

![alt text](docs/hostfile.PNG "Hostfile update status")

- Press Enter to run the test case to verify if NNMi is backed up correctly.

![alt text](docs/nnmbackup1.PNG "NNMi backup")

- Press Enter to run the test case to check NNMi status in both RPOP servers.

![alt text](docs/nnmprocess.PNG "NNMi process")

- Press Enter to run the test case to checki the NNMi version in both RPOP servers. The warning message in the screenshot can be ignored.

![alt text](docs/nnmversi.PNG "NNMi version check")

- Press Enter to run the test case to check OA in both RPOP servers.

![alt text](docs/oaverify.PNG "OA version")

- Press Enter to fetch the test reports from RPOP lite server.

- Press Enter to the display the summary of test results.

![alt text](docs/testsumm.PNG "Test report summary")

- Make sure every test results are pass.

[Back to Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)

# All

- Select option **5** to perform all the above actions.

![alt text](docs/allin.PNG "All")

- Provide the server details and credentials when prompted. Once all input is given, it displays the summary of the user input.

- Type 'y' to update the hostfile on both RPOP servers.

- Firstly, the RPOP pre-requiste checks are executed.[Click to Refer Pre-requisite steps](#pre-requisite)

- Followed by RPOP build activity.[Click to Refer Build session steps](#build)

- Finally, RPOP functionality testing is carried out.[Click to Refer Testing steps](#testing)

[Back to Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)

# Appendix

### Uninstall OA and NNMi **666** option

- 666 is a hidden option, which allows the user to uninstall all applications on both the RPOP servers. This is done based on the current configuration file that exist in GIT.
 
- Enter **666** to select the hidden option.

![alt text](docs/666in.PNG "666 option")

- Press Enter to display the existing RPOP configuration for which uninstallation needs to be done.

- Verify the server details and it prompts for confirmation to uninstall all applications.

![alt text](docs/666sum1.PNG "666 Confirm option")

- Type 'y' and press Enter to proceed with the below steps.

- It checks the host files for server details and VIP details. If anything is missed out, the script updates the details in host files of the respective servers.

- Press Enter to check whether OA is installed or not. If yes, OA would get uninstalled, else it will skip the uninstallation.

- Press Enter to proceed with OA uninstallation on both the server. 

- Press Enter to continue with NNMi version check. If NNMi is installed, then it will uninstall NNMi. 

- Both OA and NNMi uninstallation is completed on both RPOP servers.

[Back to Pre-requisites for RPOP lite build](#pre-requisites-for-rpop-lite-build)


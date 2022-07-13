![placeholder image](https://prod-discovery.edx-cdn.org/media/course/image/9efb5a34-0460-4fb3-b08d-9b0f7392765c-05e3ede66f26.png)

# Fundamentals of Operating Systems (Linux) and Virtual Machines

## Introduction

I have made a study about fundamentals of OS and how VM works.

## Use Case

- User & Hardware Interface

## Virtual Machines

 - **Virtual Machines are simply isolated systems based on host machine to boot another Operating system.**

<img width="1311" alt="Screenshot 2022-07-12 at 8 01 05 PM" src="https://user-images.githubusercontent.com/91361382/178811257-6fd43c07-9396-4adf-9931-4524fefbdb5d.png">

 - A hypervisor allows one host computer to support multiple guest VMs by virtually sharing its resources, such as memory and processing.
 - There are mainly two types of Hypervisor
   - TYPE 1
   - TYPE 2
 - The main difference between ```Type 1``` vs. ```Type 2``` hypervisors is that ```Type 1``` runs on bare metal and ```Type 2``` runs on top of an operating system. Each hypervisor type also has its own pros and cons and specific use cases.
 - ```Type 1``` is adopted by most of the companies but for personal usage, we use ```Type 2```.
 
<img width="1313" alt="Screenshot 2022-07-12 at 8 02 46 PM" src="https://user-images.githubusercontent.com/91361382/178812375-696fc773-5cb4-4ecf-91ac-9750c7123c6d.png">

- Now, we are having ```Containers``` as a light weight alternative which is now been used in cloud and DevOps in a huge scale.

## Linux Fundamentals

 - First of all, let's make it clear that Linux is not an Operating System. Rather it is a Kernel. 
 - Ubuntu, CentOS, Alpine, Kali, ParrotOS are few examples of Linux Distributions which are actual OS based on that Kernel.
 - When we boot up a Linux system, we find these existing folders. Here are the significance of those :
 
  1. /home --> Root user's home directory
  2. /bin --> Executables for most essential user commands
  3. /sbin --> System Relevant Executables (Requires Super User access)
  4. /lib --> Essential shared library that are used by executables from /bin and /sbin
  5. /usr --> User home directory (Obsolete)
  6. /usr/local --> Third party apps like Docker, Java, Minikube are installed here
  7. /opt --> Third party apps are installed which do not split data with different directories for example IDEs
  8. /boot --> System booting files
  9. /etc --> Configuration of System-wide applications are stored
  10. /dev --> Location of Device files like Keyboard, Mouse, Hardrive, etc.
  11. /var --> Contains files to which system writes data during the course of it's operation.
  12. /tmp --> Temporary resources required for the same processes
  13. /media --> Mounts removable media
  14. /mnt --> Mounts temporary file systems (Obsolete)
 
 - Files starting with dot (.) are hidden. They are also termed as dotfiles. You can view those by ticking the check box of the folder settings. Else you can try to run "ls -a" in terminal to show all files and folder including the hiddens ones.

 - Here is the list of Linux Terminal Commands prepared by myself : [Handwritten Cheatsheet.pdf](https://github.com/ronitblenz/100DaysOfCloud/files/9105455/Handwritten.Cheatsheet.pdf)

Thanks for reading till the very end.

Follow me on [Twitter](https://twitter.com/ronitblenz), [LinkedIn](https://www.linkedin.com/in/ronitbanerjee/) and [GitHub](https://github.com/ronitblenz) for more amazing blogs about Cloud, DevOps and More !


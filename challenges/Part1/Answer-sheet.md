# Part1 Answer Sheet
## 1. Create a CDH Cluster on AWS
```
a. Linux setup - i. Add the following linux accounts to all nodes
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-1.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-2.PNG?raw=true)
```
a. Linux setup - ii. List the your instances by IP address and DNS name (don’t use /etc/hosts for this)
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-3.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-4.PNG?raw=true)
```
a. Linux setup - iii. List the Linux release you are using
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-5.PNG?raw=true)
```
a. Linux setup - iv. List the file system capacity for the first node (master node)
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-6.PNG?raw=true)
```
a. Linux setup - v. List the command and output for yum repolist enabled
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-7.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-8.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-9.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-10.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-11.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-12.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-13.PNG?raw=true)
```
a. Linux setup - vi. List the /etc/passwd entries for training (only in master name node)
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-15_etc_passwd.PNG?raw=true)
```
a. Linux setup - vii. List the /etc/group entries for skcc (only in master name node)
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-15_etc_group.PNG?raw=true)
```
a. Linux setup - viii. List output of the flowing commands: 1. getent group skcc, 2. getent passwd training
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-16.PNG?raw=true)
```
b. Install a MySQl server
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-b-1.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-b-2.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-b-3.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-b-4.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-b-5.PNG?raw=true)
```
c. Install Cloudera Manager
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-1.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-2.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-3.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-4.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-5.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-6.PNG?raw=true)
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-c-7.PNG?raw=true)

```
[ 참고] CM 구성 요약
1. Check vm.swappiness on all your nodes
 1) swap 확인 
  -> sysctl vm.swappiness
 2) 영구 적용 위해 /etc/sysctl.conf 추가 필요 
  -> vi /etc/sysctl.conf --> vm.swappiness = 1 추가
2. Show the mount attributes of your volume(s)
 1) 명령어로 확인 -> df -h
3. If you have ext-based volumes, list the reserve space setting
 1) 명령어로 확인 -> fsck -a /dev/nvme0n1p1 
4. Disable transparent hugepage support
 1) cat /sys/kernel/mm/transparent_hugepage/enabled 상태확인
    [always] madvise never --> 이렇게 나오면 enabled 상태
    always madvise [never] --> 이렇게 나와야 disabled 상태
 2) sudo vi /etc/rc.d/rc.local 편집하여 아래내용 추가
    echo never > /sys/kernel/mm/transparent_hugepage/enabled
    echo never > /sys/kernel/mm/transparent_hugepage/defrag
 3) 권한 변경 -> chmod +x /etc/rc.d/rc.local 
 4) sudo vi /etc/default/grub 편집하여 아래내용 추가
    transparent_hugepage=never
 5) 명령어 실행 -> sudo grub2-mkconfig -o /boot/grub2/grub.cfg
5. List your network interface configuration
 1) ip addr 실행하여 상태확인
6. Show that forward and reverse host lookups are correctly resolved
 1) centos 계정 비밀번호 설정
   sudo passwd centos --> admin으로 통일
 2) ssh 설정 변경
   sudo vi /etc/ssh/sshd_config 편집하여 아래내용 변경
   PasswordAuthentication yes 주석 풀기
   PasswordAuthentication no 주석 처리
 3) hostname 설정
   sudo hostnamectl set-hostname 노드번호.team3.com (ex) nd1.team3.com)
 4) /etc/hosts 설정 (private IP, sudo vi로 실행)
   172.31.0.147 nd1.team3.com nd1
   172.31.2.54 nd2.team3.com nd2
   172.31.7.7 nd3.team3.com nd3
   172.31.2.235 nd4.team4.com nd4
   172.31.4.97 nd5.team5.com nd5
 5) sudo reboot 로 재시작 후 ssh로 각 노드 접속 테스트
 
7. Show the nscd service is running
 sudo yum install nscd -y
 sudo systemctl start nscd --> 서비스 시작
 systemctl status nscd -> 서비스 상태 확인
 
8. Show the ntpd service is running
 sudo yum install ntp -y
 sudo systemctl start ntpd --> 서비스 시작
 systemctl status ntpd --> 서비스 상태 확인
 
9. CM 5.15.2 Repo 설정 (모든 host)
 sudo yum install -y wget
 sudo wget https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/cloudera-manager.repo -P /etc/yum.repos.d/
 sudo vi /etc/yum.repos.d/cloudera-manager.repo 편집하여 아래내용 변경
 baseurl=https://archive.cloudera.com/cm5/redhat/7/x86_64/cm/5.15.2/

10. JDK, JDBC 설치(모든 host)
 1) jdk -> sudo yum install java-1.8.0-openjdk-devel.x86_64
 2) jdbc -> 
    wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.47.tar.gz
    tar zxvf mysql-connector-java-5.1.47.tar.gz
    sudo mkdir -p /usr/share/java/
    cd mysql-connector-java-5.1.47
    sudo cp mysql-connector-java-5.1.47-bin.jar /usr/share/java/mysql-connector-java.jar
    
11. yum Install CM (CM host)
   sudo yum install -y cloudera-manager-daemons cloudera-manager-server
  
12. Install MySQL server (CM host)
   sudo yum install -y mariadb-server
   sudo systemctl enable mariadb (안되면 재설치)
   sudo systemctl start mariadb
   sudo /usr/bin/mysql_secure_installation
 
```

## 2. In MySQL create the sample tables that will be used for the rest of the test

```
a. Linux setup - i. Add the following linux accounts to all nodes
```
![photo.PNG](https://github.com/jellybean18/SKCC_07785_FinalTest/blob/master/Images/1-a-1.PNG?raw=true)



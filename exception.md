

### 用Vagrant和VirtualBox在本地搭建分布式Kubernetes集群和Istio Service Mesh, 采坑记录



##### 1, `kubernetes-server-linux-amd64.tar.gz`版本不对，导致找不到kubectl 

​	解决：  更换kubernetes-server版本


##### 2, 没有启动dashboard服务

   解决： a.  更换docker registries, 添加阿里云源 
             b.  执行/vagrant/hack/deploy-base-services.sh 



##### 3, 2222端口冲突

  解决： 修改Vagrantfile文件后，执行`vagrant reload --provision`

    ```
      ssh_old_port = "#{i+2221}"
      ssh_port_new = "#{i+3321}"
      node.vm.network "forwarded_port", guest: 22, host: ssh_old_port, id: "ssh", disabled: "true"
      node.vm.network "forwarded_port", guest: 22, host: ssh_port_new, host_ip: "127.0.0.1"
    ```


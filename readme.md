## prereqs

git clone the repo

virtualbox - https://www.virtualbox.org/wiki/Downloads

vagrant - https://www.vagrantup.com/

## editing the vagrantfile to make fine tune to your needs

- define the image from focal64 to whatever you want, it will download first time you run vagrant up but from next time it will use the local cached image.
- hostname, pretty self explanatory
- for provider im using virtualbox but free to use whatever u want, ex. hyperV / vmware etc but might need to troubleshoot if shit doesnt work.
- adjust the vcores and memory if your host is doodoo or deploying multiple VMs

```
config.vm.define "ubuntuTEST" do |machine|
      machine.vm.box = 'ubuntu/focal64'
      machine.vm.hostname = "ubuntuTEST"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntuTEST-#{i}"
        vb.cpus = 8
        vb.memory = '8192'
```


```
vagrant up
```

```
vagrant destroy
```

```
vagrant ssh
```


# ! replace this values or edit it later in /etc/environment (do not forget logout/login after that)
namespace = 'thenamespace'
hub = 'thetopic'
key = 'thekey'

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"
    config.vm.box_check_update = false

    config.vm.provision :shell, inline: <<-SHELL
        echo "Install filebeat..."
        curl -s -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.6.0-amd64.deb
        dpkg -i filebeat-6.6.0-amd64.deb
    SHELL

    config.vm.provision :shell, inline: <<-SHELL
        echo NAMESPACE="#{namespace}" >> /etc/environment
        echo HUP="#{hub}" >> /etc/environment
        echo KEY="#{key}" >> /etc/environment

        echo "Write filebeat.yml..."
        cat /vagrant/filebeat.yml > /etc/filebeat/filebeat.yml

        echo "Provision done"
        echo "Do vagrant ssh and run sudo /usr/share/filebeat/bin/filebeat -c /etc/filebeat/filebeat.yml -e"
    SHELL
end

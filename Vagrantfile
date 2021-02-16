# Based on https://vtorosyan.github.io/ansible-docker-vagrant/
# and https://github.com/AkihiroSuda/containerized-systemd/
# and https://developers.redhat.com/blog/2016/09/13/running-systemd-in-a-non-privileged-container/
# with tweaks indicated by https://github.com/containers/podman/issues/3295
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'
Vagrant.configure("2") do |config|
  config.vm.provider "docker" do |d|
    d.build_dir       = "."
    d.has_ssh         = true
    d.remains_running = false
    d.create_args     = ['--tmpfs', '/tmp', '--tmpfs', '/run', '--tmpfs', '/run/lock', '-v', '/sys/fs/cgroup:/sys/fs/cgroup:ro', '-t']
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "test.yml"
  end
end


# -*- mode: ruby -*-
# vi: set ft=ruby :

# Licensed to Elasticsearch under one or more contributor
# license agreements. See the NOTICE file distributed with
# this work for additional information regarding copyright
# ownership. Elasticsearch licenses this file to you under
# the Apache License, Version 2.0 (the "License"); you may
# not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

Vagrant.configure(2) do |config|
  config.vm.define "jna-build" do |config|
    config.vm.box = "elastic/centos-6-x86_64"
    config.vm.provider "virtualbox" do |v|
      # Give the box 4GB because our build tools are beasts
      #v.memory = 4096
    end
    if Vagrant.has_plugin?("vagrant-cachier")
      config.cache.scope = :box
    end

    # http://foo-o-rama.com/vagrant--stdin-is-not-a-tty--fix.html
    #config.vm.provision "fix-no-tty", type: "shell" do |s|
    #  s.privileged = false
    #  s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
    #end

    config.vm.provision "shared", type: "shell", inline: configure_shared()
  end
end

def configure_shared()
  return <<-SHELL
    set -e
    yum -y install ant
    yum -y groupinstall "Development Tools"
  SHELL
end

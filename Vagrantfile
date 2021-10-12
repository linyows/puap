# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure('2') do |config|
  config.vm.define 'focal' do |m|
    m.vm.box = 'linyows/ubuntu-20.04-arm64'
    m.vm.box_version = '1.1.0'
  end

  config.vm.define 'hirsute' do |m|
    m.vm.box = 'linyows/ubuntu-21.04-arm64'
    m.vm.box_version = '1.1.0'
  end
end

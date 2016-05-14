# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

	# Use ubuntu/trusty becuase they already contain the VirtualBox drivers
	#
	# Only using 32 bits because (a) emulating 32bit machines is normally faster
	# and (b) freetz will need 32bit libraries anyway, making more difficult
	# to install on a 64bit one.
	config.vm.box = "ubuntu/trusty32"

	# 1st provision stage:
	#
	# Install the needed packages, and activate ccache
	config.vm.provision "packages", type:"shell", inline: <<-EOF
		echo 'Acquire::http::Proxy "http://10.54.5.11:3142" ;' \
		 > /etc/apt/apt.conf.d/00proxy
		export APT_FRONTEND=noninteractive
		apt-get update
		apt-get install -y build-essential \
		 vim \
		 subversion \
		 libreadline-dev \
		 libcap-dev \
		 libtool \
		 automake \
		 libncurses-dev \
		 gawk \
		 gettext \
		 pkg-config \
		 git-core \
		 python \
		 unzip \
		 bison \
		 flex \
		 imagemagick \
		 libz-dev \
		 libacl1-dev \
		 gcc-multilib \
		 curl \
		 wget \
		 realpath

	apt-get install -y ccache

	echo 'PATH=/usr/lib/ccache:$PATH' > /etc/profile.d/ccache.sh

	echo 'umask 0022' > /etc/profile.d/umask.sh

	chown vagrant:vagrant /home/vagrant/freetz
	EOF

	# 2nd provision stage: Check out freetz trunk svn
	# to $HOME/freetz
	config.vm.provision "freetz-checkout", type: "shell",
		privileged: false, inline: <<-EOF
		if [[ ! -d freetz ]] ; then
			svn checkout http://svn.freetz.org/trunk freetz
		fi
		cd freetz && svn update
	EOF

	# Use ~/freetz-images for the resulting images
	config.vm.synced_folder "images", "/home/vagrant/freetz/images"
end

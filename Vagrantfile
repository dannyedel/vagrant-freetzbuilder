# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|


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
	EOF

	config.vm.provision "freetz-checkout", type: "shell",
		privileged: false, inline: <<-EOF
		if [[ ! -d freetz ]] ; then
			svn checkout http://svn.freetz.org/trunk freetz
		fi
		cd freetz && svn update
	EOF
end

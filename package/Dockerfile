
#!BuildTag: libstorage-ng

# This actually is registry.opensuse.org/yast/head/images/opensuse/tumbleweed:latest
# when building in OBS YaST:Head!
FROM opensuse/tumbleweed

# do not install the files marked as documentation (use "rpm --excludedocs")
RUN sed -i -e "s/^.*rpm.install.excludedocs.*/rpm.install.excludedocs = yes/" /etc/zypp/zypp.conf

# import the YaST OBS GPG key
COPY YaST:Head.pub /usr/share/gpg-keys/
RUN rpm --import /usr/share/gpg-keys/YaST:Head.pub

RUN zypper addrepo --refresh http://download.opensuse.org/repositories/YaST:/Head/openSUSE_Tumbleweed yast

RUN zypper --non-interactive install --no-recommends \
  autoconf \
  automake \
  boost-devel \
  brp-check-suse \
  build \
  ccache \
  doxygen \
  gcc-c++ \
  git \
  graphviz \
  libboost_headers-devel \
  libboost_test-devel \
  libjson-c-devel \
  libtool \
  libxml2-devel \
  obs-service-source_validator \
  openSUSE-release-ftp \
  python3-devel \
  rpm-build \
  ruby-devel \
  swig \
  tack \
  && zypper clean --all \
  && rm -rf /usr/lib*/ruby/gems/*/cache/ \
  && rm -rf /usr/share/doc/ \
  && find /usr/lib/locale/* -maxdepth 1 | grep -v -E "(en_US|en_GB|cs_CZ|es_ES|de_DE|de_CH|fr_FR|C.utf8)" | xargs rm -rf \
  && find /usr/share/locale -name "*.mo" -delete

ENV LC_ALL=en_US.UTF-8
WORKDIR /usr/src/app


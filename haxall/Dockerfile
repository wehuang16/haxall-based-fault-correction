# ### Haxall https://github.com/haxall/haxall
# ### Create a clean Ubuntu container with Haxall
# ### Author: Chris Weyandt (cweyandt@lbl.gov)
# ### Created: 2022-11-30

# Load base image from Ubuntu
FROM ubuntu

# Basic updating & utility installation
RUN apt update
RUN apt install -y wget unzip vim-tiny default-jdk 
RUN apt install -y git


# Install Fantom
# https://fantom.org/doc/docTools/Setup
WORKDIR /tmp
RUN wget https://github.com/fantom-lang/fantom/releases/download/v1.0.78/fantom-1.0.78.zip
RUN mkdir /apps
RUN unzip fantom-1.0.78.zip -d /apps/
WORKDIR /apps/fantom-1.0.78/
RUN chmod +x ./adm/unixsetup
RUN ./adm/unixsetup
ENV PATH=${PATH}:/apps/fantom-1.0.78/bin


# Build Haystack-Defs
# https://haxall.io/doc/docHaxall/Build
WORKDIR /
RUN git clone https://github.com/Project-Haystack/haystack-defs.git
WORKDIR /haystack-defs
RUN touch fan.props
RUN ./src/build.fan

# Build Haxall
# https://haxall.io/doc/docHaxall/Build
WORKDIR /
RUN git clone https://github.com/haxall/haxall.git
WORKDIR /haxall
RUN echo path=/haystack-defs > fan.props
# Next line is risky, since JDK was installed as "default-jdk" above and will depend on the host machine arch
ENV FAN_BUILD_JDKHOME=/usr/lib/jvm/java-11-openjdk-amd64/
RUN ./src/build.fan
RUN chmod +x /haxall/bin/*
ENV PATH=${PATH}:/haxall/bin
WORKDIR /haxall/bin
# RUN fan hx init demo  # Cannot init demo because it is interactive
CMD fan hx run demo

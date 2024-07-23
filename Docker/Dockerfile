# Use Ubuntu 20.04 as the base image
FROM ubuntu:20.04

#############  Common setup commands required by most environments #############
# Update sources
RUN apt update \
    # Set up timezone
    && DEBIAN_FRONTEND=noninteractive apt install -y tzdata \
    && ln -fs /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    # Install software-properties-common package for 'add-apt-repository'
    && apt install -y software-properties-common \
    # Enable 'partner' repository
    && add-apt-repository "deb http://archive.canonical.com/ubuntu focal partner" \
    # Install build tools
    && apt install -y build-essential cmake \
    # Upgrade packages
    && apt -y upgrade \
    # Create the user (-m: create home directory if does not exist)
    && groupadd --gid 1000 user \
    && useradd --uid 1000 --gid user -m user \
    # Add sudo support
    && apt install -y sudo \
    && echo user ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/user \
    && chmod 0440 /etc/sudoers.d/user

# Set the default user to the defined user
USER user

# Set the CWD
WORKDIR /home/user/workdir

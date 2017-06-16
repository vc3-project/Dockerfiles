FROM lincolnbryant/gentoo-rap-base:latest
MAINTAINER Lincoln Bryant <lincolnb@uchicago.edu>

USER build
WORKDIR /home/build

# Export the environment. This should make it easy to redefine at runtime
ENV PATH "$EPREFIX/usr/bin:$EPREFIX/bin:$EPREFIX/tmp/usr/bin:$EPREFIX/tmp/bin:/usr/bin:/bin"

# Test
RUN emerge gromacs

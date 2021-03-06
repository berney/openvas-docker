OpenVAS image for Docker
==============

[![Circle CI](https://img.shields.io/circleci/project/mikesplain/openvas-docker/master.svg)](https://circleci.com/gh/mikesplain/openvas-docker/tree/master) [![Docker Pulls](https://img.shields.io/docker/pulls/mikesplain/openvas.svg)](https://hub.docker.com/r/mikesplain/openvas/) [![Docker Stars](https://img.shields.io/docker/stars/mikesplain/openvas.svg)](https://hub.docker.com/r/mikesplain/openvas/) [![](https://images.microbadger.com/badges/image/mikesplain/openvas.svg)](https://microbadger.com/images/mikesplain/openvas "Get your own image badge on microbadger.com")

A Docker container for OpenVAS on Ubuntu.  By default, the latest images includes the OpenVAS Base as well as the NVTs and Certs required to run OpenVAS.  We made the decision to move to 9 as the default branch since 8 seems to have [many issues](https://github.com/mikesplain/openvas-docker/issues/84) in docker.  We suggest you use 9 as it is much more stable. Our Openvas9 build was designed to be a smaller image with fewer extras built in. In coming weeks, we'll look at adding some extras back in.

We currently package 2 versions:

| Openvas Version | Tag     | Web UI Port |
|-----------------|---------|-------------|
| 9               | latest/9| 4000        |
| 8               | 8       | 443         |



Usage
-----

Simply run:

```
# 9
docker run -d -p 4000:4000 --name openvas mikesplain/openvas:9
# 8
docker run -d -p 443:443 --name openvas mikesplain/openvas:8
```

This will grab the container from the docker registry and start it up.  Openvas startup can take some time (4-5 minutes while NVT's are scanned and databases rebuilt), so be patient.  Once you see a `It seems like your OpenVAS-9 installation is OK.` process in the logs, the web ui is good to go.  Goto `https://<machinename>(and :4000 for v9)`

```
Username: admin
Password: admin
```

To check the status of the process, run:

```
docker top openvas
```

In the output, look for the process scanning cert data.  It contains a percentage.

To run bash inside the container run:

```
docker exec -it openvas bash
```

Contributing
------------

I'm always happy to accept [pull requests](https://github.com/mikesplain/openvas-docker/pulls) or [issues](https://github.com/mikesplain/openvas-docker/issues).

Thanks
------
Thanks to hackertarget for the great tutorial: http://hackertarget.com/install-openvas-7-ubuntu/
Thanks to Serge Katzmann for contributing with some great work on OpenVAS 8: https://github.com/sergekatzmann/openvas8-complete

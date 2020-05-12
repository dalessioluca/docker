# docker

The docker images will appear here:
https://console.cloud.google.com/gcr/images/broad-dsde-methods/US

They can be used in WDL by typing:
runtime {
  docker: "us.gcr.io/broad-dsde-methods/pyro_matplotlib:1.3.0"
  bootDiskSizeGb: 50
  ....
  }

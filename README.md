## The Hello Forge Service

The hello forge service is a simple flask application that reports its
uptime. This is useful for illustrating the principles of building a
service with forge.

### Key Files

Forge looks at these files to build and deploy the edge service:

 - service.yaml

   This identifies this directory as a service. It also contains
   parameters that are supplied to the deployment templates. In this
   case that consists of the service name, the port the container
   exposes, and the minimum memory and cpu required by the
   application.

   Any additional configuration information supplied in this file is
   made available to the deployment templates. This is useful if you
   want to develop fancier custom deployment templates and make them
   easily configurable via parameters in service.yaml.

 - Dockerfile

   This tells forge how to build the service. You can replace this
   with a different Dockerfile if you want to use a different
   application framework, or replace this edge service with a
   prepackaged API gateway like [ambassador](http://getambassador.io).

 - k8s/*

   This directory contains the templates forge uses to produce the
   kubernetes yaml necessary to deploy a service. They can be
   customized on a per service basis as needed. The templates are also
   [jinja](http://jinja.pocoo.org/docs/2.9/templates/)
   templates. Please refer to the
   [jinja](http://jinja.pocoo.org/docs/2.9/templates/) documentation
   for the full syntax.

   When these templates are instantiated, they are supplied with all
   the parameters in service.yaml as well as all the metadata from the
   build.  This currently consists of the built image names
   corresponding with each Dockerfile the service uses.

   The service parameters are supplied to the deployment templates
   under the `service` variable name. The build metadata is supplied
   under the `build` variable name, and the docker images are
   available in the `build.images` map. This map is keyed by path
   relative to the directory containing the service.yaml file.

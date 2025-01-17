.. image:: https://img.shields.io/badge/chat-matrix.org-blue.svg
   :alt: Matrix
   :target: https://riot.im/app/#/room/#reprozip:matrix.org

ReproServer
===========

Goals
-----

- Import something we can build a Docker image from (currently only a ReproZip package)
- Build a Docker image from it
- Allow the user to change experiment parameters and input files
- Run the experiment
- Show the log and output files to the user

How to run this with Tilt
-------------------------

Make sure you have checked out the submodule with ``git submodule init && git submodule update``

You will need `Tilt <https://docs.tilt.dev/install.html>`__, `kubectl <https://kubernetes.io/docs/tasks/tools/>`__, and a cluster with a local registry (that you can set up with `ctlptl <https://github.com/tilt-dev/ctlptl>`__).

For example, create a local cluster with::

    ctlptl create cluster minikube --registry=ctlptl-registry --kubernetes-version=v1.22.2

Install the ingress controller using::

    kubectl apply -f k8s/nginx-ingress.k8s-1.22.yml

Start the application for development using::

    tilt up

You can then open `http://localhost:8000/ <http://localhost:8000/>`__ in your browser. Tilt will automatically rebuild images and update Kubernetes as you make changes.

How to run this with docker-compose
-----------------------------------

You will need `Docker <https://hub.docker.com/search/?type=edition&offering=community>`__ and `docker-compose <https://docs.docker.com/compose/install/>`__.

- Make sure you have checked out the submodule with ``git submodule init && git submodule update``
- Copy ``env.dist`` to ``.env`` (you probably don't need to change the settings)
- Start services by running ``docker-compose up -d --build``
- Open `localhost:8000 <http://localhost:8000/>`__ in your browser

How to stop it: ``docker-compose down -v``

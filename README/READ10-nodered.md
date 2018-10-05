# Node-RED Docker help

Using the Node-RED Docker Official image, README [here](https://github.com/node-red/node-red-docker/blob/master/README.md).

## Adding mode Nodes to the Standard template

In the README, it shows how to do this in the Container Shell, [here](https://github.com/node-red/node-red-docker/blob/master/README.md#container-shell).

Do it with Ansible:

```
vars:
  cntr_name: "rhm_nrtest_1"

with_items:
  - cd /data
  - npm install node-red-node-smooth
  - node-red-node-smooth@0.0.3 node_modules/node-red-node-smooth
  - exit
  - docker stop mynodered
  - docker start mynodered
```

## New

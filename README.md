# displacement-ts-server-terraform
Used to automatically setup a leaflet displacement time series server for configured HySDS/ARIA system

## Requirements
1. Install [Terraform](https://www.terraform.io/) onto Mozart machine.
1. If you are using AWS, make sure you have your credentials setup up. 
   - To set them up, install the [AWS CLI](https://aws.amazon.com/cli/) and run `aws configure`.
1. Complete setup of [HySDS core](https://hysds-core.atlassian.net/wiki/spaces/HYS/pages/18284549/Installation) with ARIA adaptaion (i.e. [leaflet-ingester job](https://github.com/aria-jpl/leaflet-ingester/tree/dev))
1. Needed repos for functionality:
   - [displacement-ts-server](https://github.com/aria-jpl/displacement-ts-server/tree/dev)
   - [leaflet-ingester](https://github.com/aria-jpl/leaflet-ingester/tree/dev)

## Usage
1. Log into Mozart and clone repo
   ```
   mkdir ~/tss_server
   cd ~/tss_server
   git clone https://github.com/hysds/hysds-terraform.git -b leaflet_server
   cd hysds-terraform
   ```
1. Copy the variables.tf.tmpl to variables.tf:
   ```
   cp variables.tf.tmpl variables.tf
   ```
   1. Initialize so plugins are installed:
   ```
   terraform init
   ```
1. Update the values starting with two underscores, e.g. \_\_region\_\_, for your provider account and settings. Edit the variables.tf file with custom variables for this installation venue. Many of these values can be acquired from the aws console.
   ```
   vi variables.tf
   ```
1. Determine the `project`, `venue` and `counter` for your HySDS cluster. They will be used to uniquely name and identify your cluster's resources.
   - `project` e.g. swot, smap, aria, grfn, eos
   - `venue` e.g. ops, dev, test, gerald
   - `counter` e.g. 1, 2, 3
1. Validate your configuration:
   ```
   terraform validate --var project=aria --var venue=ops --var counter=1
   ```
1. Build your HySDS clustser:
   ```
   terraform apply --var project=aria --var venue=ops --var counter=1
   ```
1. Show status of your HySDS cluster:
   ```
   terraform show --var project=aria --var venue=ops --var counter=1
   ```
1. Destroy your HySDS cluster once it's no longer needed:
   ```
   terraform destroy --var project=aria --var venue=ops --var counter=1
   ```

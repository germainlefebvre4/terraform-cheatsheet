# Terraform CheatSheet
A usefull cheatsheet for Terraform usage.
Written by Germain LEFEBVRE by August 2018 from Terraform v0.11.7.

**Table of Contents**
1. [Context](#context)
1. [Terraform Commands](#terraform-commands)
1. [Terraform configuration management](#terraform-configuration-management)
   1. [Global variables](#global-variables)
   1. [Environment management](#environment-management)
   1. [Requiring variables](#requiring-variables)
   1. [Environments variables](#eenvironments-variables)

## Context

See version of Terraform with `terraform --version` :
```
Terraform v0.11.7
```

## Terraform commands

The first step to know is all your structure will be store in a `main.tf` file in your current directory.


These are the main Terraform commands.

Show Terraform help.

`terraform --help`

```
Usage: terraform [--version] [--help] <command> [args]
```


Initiliaze your Terraform directory (1st step needed with new directory).
`terraform init`


Validate your Terraform files, coherence in structure but no syntax checking.

`terraform validate`


See what Terraform will change but not applying any change.

`terraform plan`


Apply modifications on your infrastructure.

`terraform apply`


Remove all your modifications (made with apply).
`terraform destroy`


## Terraform configuration management

### Global variables
With the art of calling all your resources from a `main.tf` file you will have a another files containing all your variables.
The file name does not matter while your call it with the `.tf` extension. Whatever the way your name it, variables.tf or vars.tf, it will be call while it remains in the same directory of your `main.tf` file.
```
./
 +-- main.tf
 +-- vars.tf
```

### Environment management
Take care to your configuration files if your want to manage different environments becasue it will change regarding the way your wnat to handle it.

I have a particular preference for managing config files with files but no workspace because everything is files in Linux.
To do so you will pay attention to seprate every environments in different files (dev, sit, qa, prod, ...).

#### Requiring variables
The main thing to know is you need a global variables file to specify your required variables. As requiring vars file I mean the Global variables files described just above.

#### Environments variables
After describing requiring variables you can play in creating structure by environment (directories) and setup a file with your environment vars. The name of this file does not matter in a chaos way. But if you want to make automation I suggest you to name the env files exactly the same in all your env directories.

Considering your resource file named `main.tf`and your global vars file name `variables.tf` you wil have a file structure like this :
```
./
+-- dev/
    +-- vars.tf
+-- prod/
    +-- vars.tf
+-- main.tf
+-- variables.tf
```

Like this files `main.tf` and `variables.tf` wil be called at every `terraform` run. You will just need to specify your environment file with the parameter `-var-file=<you_file>` :

`terraform plan -var-file=./dev/vars.tf`



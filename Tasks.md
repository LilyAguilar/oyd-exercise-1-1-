Universidad Galileo

PDDS

Optimizaciones y desempeño

Lilian Aguilar

# Task 1

```shell
> terraform init
Initializing the backend...
Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 5.0"...
- Installing hashicorp/aws v5.100.0...
- Installed hashicorp/aws v5.100.0 (signed by HashiCorp)
Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

```shell
> terraform validate
Success! The configuration is valid.
```

# Task 2

```shell
>terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
following symbols:
  + create

Terraform will perform the following actions:

  # aws_s3_bucket.exercise will be created
  + resource "aws_s3_bucket" "exercise" {
      + acceleration_status         = (known after apply)
      + acl                         = (known after apply)
      + arn                         = (known after apply)
      + bucket                      = "oyd-exercise-bucket-2026"
      + bucket_domain_name          = (known after apply)
      + bucket_prefix               = (known after apply)
      + bucket_regional_domain_name = (known after apply)
      + force_destroy               = false
      + hosted_zone_id              = (known after apply)
      + id                          = (known after apply)
      + object_lock_enabled         = (known after apply)
      + policy                      = (known after apply)
      + region                      = (known after apply)
      + request_payer               = (known after apply)
      + tags                        = {
          + "Environment" = "dev"
          + "ManagedBy"   = "terraform"
        }
      + tags_all                    = {
          + "Environment" = "dev"
          + "ManagedBy"   = "terraform"
        }
      + website_domain              = (known after apply)
      + website_endpoint            = (known after apply)

      + cors_rule (known after apply)

      + grant (known after apply)

      + lifecycle_rule (known after apply)

      + logging (known after apply)

      + object_lock_configuration (known after apply)
      + logging (known after apply)

      + object_lock_configuration (known after apply)

      + replication_configuration (known after apply)

      + logging (known after apply)

      + object_lock_configuration (known after apply)

      + replication_configuration (known after apply)
      + replication_configuration (known after apply)


      + server_side_encryption_configuration (known after apply)
      + server_side_encryption_configuration (known after apply)

      + versioning (known after apply)

      + website (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

---

# Task 2

1. **How many resources will be created, changed, or destroyed?**
   - Creados: 1
   - Modificados: Ninguno
   - Destruidos: Ninguno

2. **What does the + symbol next to each attribute mean?**

   Indica que es un nuevo archivo que se va a crear.

3. **Find one attribute in the plan marked as (known after apply). Why can't Terraform know that value before apply?**

   Terraform no conoce estos valores porque son generados por AWS, no por Terraform.

# Task 3

```shell
  # aws_s3_bucket.exercise will be created
  + resource "aws_s3_bucket" "exercise" {
      + acceleration_status         = (known after apply)
      + acl                         = (known after apply)
      + arn                         = (known after apply)
      + bucket                      = "oyd-exercise-bucket-2026"
      + bucket_domain_name          = (known after apply)
      + bucket_prefix               = (known after apply)
      + bucket_regional_domain_name = (known after apply)
      + force_destroy               = false
      + hosted_zone_id              = (known after apply)
      + id                          = (known after apply)
      + object_lock_enabled         = (known after apply)
      + policy                      = (known after apply)
      + region                      = (known after apply)
      + request_payer               = (known after apply)
      + tags                        = {
          + "Environment" = "dev"
          + "ManagedBy"   = "terraform"
          + "Owner"       = "your-name"
        }
      + tags_all                    = {
          + "Environment" = "dev"
          + "ManagedBy"   = "terraform"
          + "Owner"       = "your-name"
        }
      + website_domain              = (known after apply)
      + website_endpoint            = (known after apply)

      + cors_rule (known after apply)

      + grant (known after apply)

      + lifecycle_rule (known after apply)

      + logging (known after apply)

      + object_lock_configuration (known after apply)

      + replication_configuration (known after apply)

      + server_side_encryption_configuration (known after apply)

      + versioning (known after apply)

      + website (known after apply)
    }
```


1. __Did Terraform propose to destroy and recreate the bucket, or update it in place?__

   Terraform propone crearlo desde cero.
3. __Why does that distinction matter?__

   Esto significaría que el bucket actual se borraría por completo lo que implica perder todos los archivos y objetos almacenados dentro.


# Task 4
No existe el archivo `.tfstate`
```shell
> ls -la

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        23/04/2026     20:25                .terraform
-a----        23/04/2026     20:26           1407 .terraform.lock.hcl
-a----        23/04/2026     22:08            383 main.tf
-a----        23/04/2026     20:25             29 mise.toml
-a----        23/04/2026     22:15           6146 Tasks.md
```
1. __What does the absence (or presence) of the state file tell you about the relationship between plan and state?__

    Indica que el plan no es más que una propuesta, no modifica nada hasta que no se ejecute _apply_

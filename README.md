# Despliegue de Aplicación con Terraform y Ansible

# Ejecución del proyecto

## Ejecutar pruebas

```bash
cd app
pytest
```

## Ejecutar terraform

```bash
cd terraform
terraform init
terraform validate
terraform apply -auto-approve -var="private_key_path=/ruta/tu_clave.pem"
```


## Ejecutar Ansible

```bash
cd ansible
ansible-playbook -i inventory playbook.yml
```

## Acceder a la app

```bash
http://IP_PUBLICA:5000/
```

## Destruir la infraestructura

```bash
terraform destroy -auto-approve -var="private_key_path=/ruta/tu_clave.pem"
```
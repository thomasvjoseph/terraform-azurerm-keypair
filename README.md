# terraform-azurerm-keypair
Terraform Azure RM SSH KeyPair Module

## Usage

```hcl
module "key_pair" {
  source                    = "thomasvjoseph/keypair/azurerm"
  version                   = "1.x.x"
  location                  = "eastus"
  resource_group_name       = "my-resource-group"
  key_pair_name             = "my-key-pair"
  rsa_bits                  = 2048  # Optional, defaults to 4096
}
```

This module will create an AWS key pair using the provided `key_pair_name` and generate an RSA private key with the specified `rsa_bits`.

## Resources

- `azurerm_ssh_public_key` – Manages a SSH Public Key.
- `tls_private_key` – Generates a private key with the provided RSA bits.
- `local_file` – Writes the private key to a `.pem` file on your local system.

## Inputs

| Name                  | Description                                             | Type     | Default | Required |
|-----------------------|---------------------------------------------------------|----------|---------|----------|
| `resource_group_name` | The name of the Resource Group where the SSH Public Key | `string` | n/a     | yes      |
| `location`            | The Azure Region where the SSH Public Key               | `string` | n/a     | yes      |
| `key_pair_name`       | The name of the key pair                                | `string` | n/a     | yes      |
| `rsa_bits`            | Number of bits for RSA key generation                   | `number` | 4096    | no       |

## Outputs

| Name              | Description                          |
|-------------------|--------------------------------------|
| `key_pair_name`   | The name of the generated key pair   |
| `private_key_path`| The path to the private key file     |
| `ssh_public_key`  | The SSH Public Key                   |


After applying the Terraform configuration, the private key will be saved via any CI/CD pipeline `my-new-key.pem` 
example github actions:

## Examples
```yml
    - name: Upload PEM file
        if: contains(github.event.head_commit.message, 'keypair')
        uses: actions/upload-artifact@v4
        with:
          name: pem-file
          path: environments/dev/hello-module.pem #specify the path name and key file name
```
## License

This module is licensed under the MIT License.

## Author:  
thomas joseph
- [linkedin](https://www.linkedin.com/in/thomas-joseph-88792b132/)
- [medium](https://medium.com/@thomasvjoseph)
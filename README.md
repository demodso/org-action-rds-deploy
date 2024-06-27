# RDS Deploy Action

This GitHub Action deploys a PostgreSQL RDS instance on AWS using Terraform.

## Inputs

- `aws_region`: AWS region to deploy the RDS instance (default: 'ap-southeast-2')
- `instance_class`: RDS instance class (default: 'db.t3.micro')
- `db_name`: Name of the database to create
- `db_username`: Master username for the RDS instance
- `db_password`: Master password for the RDS instance
- `db_instance_name`: Name tag for the RDS instance (default: 'Demo RDS Instance')

## Outputs

- `rds_endpoint`: The connection endpoint for the RDS instance
- `rds_port`: The port the RDS instance is listening on

## Usage

```yaml
- name: Deploy RDS Instance
  uses: demodso/org-action-rds-deploy@v1
  with:
    aws_region: "ap-southeast-2"
    instance_class: "db.t3.micro"
    db_name: "mydb"
    db_username: ${{ secrets.DB_USERNAME }}
    db_password: ${{ secrets.DB_PASSWORD }}
    db_instance_name: "My RDS Instance"
```

## Prerequisites

AWS credentials: This action assumes that AWS credentials are already configured in your workflow. We recommend using OIDC for secure, short-term credentials. See Configuring OpenID Connect in Amazon Web Services for more information.
IAM Permissions: Ensure that the IAM role or user associated with the AWS credentials has the necessary permissions to create and manage RDS instances.

## Security Considerations

Always use secrets for sensitive information like database passwords. Never hard-code these values in your workflow files.
The action creates a security group that allows inbound traffic on port 5432 (default PostgreSQL port) from anywhere (0.0.0.0/0). In a production environment, you should restrict this to specific IP ranges or security groups.

## Customization

This action uses Terraform to deploy the RDS instance. If you need to customize the deployment beyond what's provided by the input parameters, you can fork this repository and modify the Terraform files as needed.

## Contributing

Contributions to improve this action are welcome. Please submit a pull request with your proposed changes.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

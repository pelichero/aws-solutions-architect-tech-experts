# Soluções

## SOLUÇÃO DO DESAFIO

Esta solução permite copiar e colar cada comando para concluir com êxito a tarefa. Verifique se você entendeu o que cada comando faz para garantir que possa aplicar o que aprendeu aos ambientes da AWS gerenciados.

Para essa solução, você cria a política do IAM que concede as permissões para a instância do Amazon EC2 usando a AWS CLI. Você deve criar o arquivo JSON que define a política do IAM. Este exemplo usa o comando `cat` para ecoar texto em um arquivo.

Crie um arquivo com o objeto de política JSON e nomeie o arquivo como `ReadOnlyPolicy.json` executando o seguinte comando:

```
cat <<EOF >> ~/ec2ReadOnlyPolicy.json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*",
                "rds:Describe*",
                "sts:AssumeRole"
            ],
            "Resource": "*"
        }
    ]
}
EOF
```

Crie uma nova política usando o documento de política que você criou anteriormente executando o seguinte comando:

```
aws iam create-policy --policy-name ec2ReadOnlyPolicy --policy-document file://ec2ReadOnlyPolicy.json
```

O comando `aws iam create-policy` produz várias informações, incluindo o ARN da política do IAM. A aparência do ARN deve ser semelhante à seguinte:

```
arn:aws:iam::<AccountId>:policy/ec2ReadOnlyPolicy
```

Copie a saída ARN do comando em um editor de texto para usar mais tarde.

Obtenha o nome da função `ec2ReadOnlyRole` e o ID da conta da AWS executando os seguintes comandos:

```
ec2ReadOnlyRole=$(aws iam list-roles --query 'Roles[*].[RoleName]' --output text | grep ec2ReadOnlyRole)
echo $ec2ReadOnlyRole
accountId=$(aws sts get-caller-identity --query 'Account' --output text)
echo $accountId
```

Saiba mais: A saída de cada comando está sendo salva como uma variável usada nos comandos subsequentes. Isso facilita o desenvolvimento de scripts quando você opera em escala e reduz o número de substituições necessárias para essa solução.

Anexe a política que você criou anteriormente à função do IAM `ec2ReadOnlyRole` executando o seguinte comando:

```
aws iam attach-role-policy --role-name $ec2ReadOnlyRole --policy-arn <PolicyArn>
```

Importante: Substitua `<PolicyArn>` pelo valor que você copiou em uma das etapas anteriores.

Suponha a função do IAM executando o seguinte comando:

```
aws sts assume-role --role-arn "arn:aws:iam::$accountId:role/$ec2ReadOnlyRole" --role-session-name AWSCLI-Session
```

Este comando não funcionará. Você deve primeiro atualizar a política de confiança antes de poder assumir a função. Para atualizar a política de confiança, você precisa do `InstanceId`.

Encontre o `InstanceId` executando o seguinte comando:

```
ec2InstanceId=$(aws ec2 describe-instances --query 'Reservations[*].Instances[*].{Instance:InstanceId}' --filters Name=instance-state-name,Values=running --output text)
echo $ec2InstanceId
```

Crie um arquivo com a relação de confiança atualizada executando o seguint

e comando:

```
cat <<EOF >> ~/TrustRelationship.json
{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "AWS": [
                    "arn:aws:sts::$accountId:assumed-role/$ec2ReadOnlyRole/$ec2InstanceId",
                    "arn:aws:iam::$accountId:root"
                    ]
                },
                "Action": "sts:AssumeRole"
            }
        ]
}
EOF
```

Anexe o documento de relação de confiança à função executando o seguinte comando:

```
aws iam update-assume-role-policy --role-name $ec2ReadOnlyRole --policy-document file://TrustRelationship.json
```

Solicitar credenciais para assumir a função executando o seguinte comando:

```
aws sts assume-role --role-arn "arn:aws:iam::$accountId:role/$ec2ReadOnlyRole" --role-session-name AWSCLI-Session
```

O comando AWS CLI produz várias informações. Dentro do bloco de credenciais, você precisa de `SecretAccessKey`, `SessionToken` e `AccessKeyId`. Para usar a nova função, você precisa criar variáveis ambientais que contenham a saída de informações pelo comando anterior.

Crie as três variáveis de ambiente a seguir para assumir a função do IAM atualizando e executando os seguintes comandos:

```
export AWS_SECRET_ACCESS_KEY=<SecretAccessKey>
export AWS_SESSION_TOKEN=<SessionToken>
export AWS_ACCESS_KEY_ID=<AccessKeyId>
```

Importante: Substitua `<SessionToken>`, `<SecretAccessKey>` e `<AccessKeyId>` com os valores de saída na etapa anterior.

Verifique se você assumiu a função do IAM executando este comando:

```
aws sts get-caller-identity
```

O resultado indica que agora você está usando a função `ec2ReadOnlyRole`.

Verifique se as permissões são diferentes executando o seguinte comando:

```
aws rds describe-db-instances --query "DBInstances[*].[DBInstanceIdentifier, DBName, DBInstanceStatus, AvailabilityZone, DBInstanceClass]" --output table
```

O comando é concluído com êxito.

Alterne para a função original executando o seguinte comando:

```
unset AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY AWS_SESSION_TOKEN
```

Verifique se você está usando a função original executando o seguinte comando:

```
aws sts get-caller-identity
```

Use o tempo restante para criar uma política CRUD, anexá-la à função `ec2CRUDRole` e verifique se você pode encerrar a instância à qual está conectado.
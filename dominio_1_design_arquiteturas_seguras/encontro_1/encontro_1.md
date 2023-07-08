# Design de arquiteturas seguras - 2 encontro 

## Sobre users e roles

##### Crie as credenciais para acesso via cli

Listar grupo
```
aws iam list-groups-for-user --user-name fepelichero
```

Assumir role
```
aws sts assume-role --role-arn arn:aws:iam::741633597846:role/role-to-do-nothing --role-session-name MySession
```

Assumir a role:
```
export AWS_SECRET_ACCESS_KEY=<SecretAccessKey>
export AWS_SESSION_TOKEN=<SessionToken>
export AWS_ACCESS_KEY_ID=<AccessKeyId>
```

Listar grupo
```
aws s3 ls
```

Revogar role

```
unset AWS_ACCESS_KEY_ID AWS_SECRET_ACCESS_KEY AWS_SESSION_TOKEN
```

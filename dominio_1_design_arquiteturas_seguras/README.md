# Dominio 1: Design de arquiteturas seguras.


## IAM (Identity and Access Management)

## 1. IAM - Manutenção de Acessos

A IAM do AWS permite que você gerencie com precisão as permissões de acesso dos usuários aos recursos do AWS. Com a IAM, você pode criar e gerenciar identidades de usuário e conceder ou negar permissões de acesso a recursos.

- Crie e gerencie usuários, grupos e funções.
- Defina políticas de acesso granulares para recursos específicos.
- Gerencie as credenciais de segurança dos usuários.

## 2. IAM - Segurança e Conformidade

A IAM é uma ferramenta fundamental para a segurança e conformidade em sua organização AWS. Com a IAM, você pode:

- Aplicar o princípio de "privilégios mínimos" ao conceder acesso a recursos.
- Monitorar e auditar as ações realizadas por usuários e funções.
- Integrar com outros serviços da AWS para reforçar a segurança.

## 3. IAM - Assumir Papéis

A funcionalidade de "Assumir Papéis" da IAM permite que você delegue temporariamente permissões de acesso a usuários, serviços ou contas da AWS. Isso é útil para cenários em que você precisa conceder acesso a recursos específicos sem fornecer credenciais permanentes.

- Crie e configure funções de confiança para assumir papéis.
- Delegue permissões para usuários e serviços assumirem esses papéis.
- Estabeleça relações de confiança entre contas da AWS.

## 4. IAM - Web Federation

A funcionalidade de "Web Federation" da IAM permite que você integre a autenticação e autorização com serviços de identidade externos. Isso é útil para permitir que os usuários usem suas credenciais existentes para acessar recursos da AWS.

- Configure a federação da Web com provedores de identidade externos.
- Permita que os usuários façam login usando suas contas corporativas.
- Forneça acesso seguro a recursos da AWS usando identidades externas.

## 5. IAM - Lógica de Avaliação de Política

As políticas da IAM são escritas usando uma linguagem de lógica de avaliação de políticas que define as permissões de acesso. Essa linguagem permite que você especifique condições lógicas para controlar com precisão o acesso aos recursos.

- Use elementos lógicos, como condições IF/THEN, para definir permissões.
- Especifique atributos de contexto, como endereços IP e horários de acesso.
- Defina políticas granulares para recursos específicos.

## 6. IAM - Introdução a Organizações

O AWS Organizations é um serviço que permite consolidar várias contas da AWS em uma única organização. A IAM é usada para gerenciar acesso e permissões em uma estrutura organizacional.

- Crie e gerencie unidades organizacionais (OUs) para estruturar sua organização.
- Defina políticas de serviço e recursos em nível de organização.
- Simplifique a gestão centralizada de várias contas da AWS.

## 7. IAM - Configurar Múltiplas Contas e Melhores Práticas com IAM Organizações

A configuração de várias

 contas com o uso do serviço IAM Organizações é uma prática recomendada para melhorar a segurança e a governança na AWS. Além disso, permite que você gerencie recursos e permissões em toda a organização.

- Crie e gerencie várias contas da AWS usando IAM Organizações.
- Defina políticas e permissões em nível de organização.
- Aplique as melhores práticas de segurança e governança em toda a organização.

## 8. IAM - AWS Control Tower

O AWS Control Tower é um serviço que oferece recursos para configurar e governar uma estrutura segura e bem gerenciada na AWS. A IAM é usada para definir e gerenciar permissões e acesso nos recursos configurados pelo Control Tower.

- Configure e implante um ambiente seguro com as configurações padrão do Control Tower.
- Defina políticas de acesso e permissões em nível de conta usando a IAM.
- Mantenha a conformidade e aplique as melhores práticas fornecidas pelo Control Tower.



## Links 

https://aws.amazon.com/blogs/security/top-10-security-items-to-improve-in-your-aws-account/
https://aws.amazon.com/cognito/
https://aws.amazon.com/directoryservice/?c=sc&sec=srv
https://aws.amazon.com/iam/
https://aws.amazon.com/iam/identity-center/
https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-scenarios.html
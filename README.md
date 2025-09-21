# Book Organization System with AWS
Este repositório explora o uso de instâncias EC2 e EBS na AWS para implementar uma arquitetura simples de um sistema de organização e avaliação de livros lidos por um usuário. O sistema permite catalogar, classificar e avaliar livros, com foco em escalabilidade, segurança e integração com serviços AWS.

## Seleção de Instância EC2

Para um sistema simples de organização de livros, instâncias do tipo t3.micro ou t3.small são adequadas devido ao baixo custo e à capacidade suficiente para processamento moderado.
A escolha do tipo de instância deve considerar a necessidade de memória (para armazenamento de metadados de livros) e CPU (para processamento de avaliações e buscas).

## Uso de Amazon Machine Images (AMIs)

Utilizar AMIs pré-configuradas com sistemas operacionais (Amazon Linux) e software necessário agiliza a criação do sistema.
Para consistência, criar uma AMI personalizada com a configuração do sistema após otimização.

## Armazenamento via Amazon EBS

Usar volumes EBS para armazenar dados da aplicação e do banco de dados. Para sistemas pequenos (nosso caso), um volume GP3 (SSD) de 20-50 GB é suficiente.
Implementar snapshots EBS para backup regular dos dados dos livros e avaliações.

## Gerenciamento com AWS Systems Manager

Systems Manager Agent (SSM Agent) já vem pré-instalado em AMIs da Amazon Linux.

##Escalabilidade com EC2 Auto Scaling

Para tráfego variável (ex.: picos durante atualizações de biblioteca), configurar EC2 Auto Scaling para escalar horizontalmente baseado em métricas de CPU ou requisições.
Usar um Application Load Balancer para distribuir tráfego entre instâncias.

## Integração com Serviços AWS

- Amazon RDS: Para armazenar metadados dos livros e avaliações, usar Amazon RDS (MySQL ou PostgreSQL) em vez de instalar DB na EC2, para melhor gerência e backup.
- Amazon S3: Armazenar capas de livros ou exportações de biblioteca em S3 para reduzir carga na EC2.
- AWS Lambda: Funções serverless para processamento assíncrono, como geração de relatórios de leitura.

## Monitoramento com Amazon CloudWatch

Coletar métricas da EC2 (CPU, memória, disco) e alarmes para notificação de problemas.

## Economia de Custos

Usar instâncias Spot para workloads não críticas (ex: processamento de backups) para reduzir custos.
Reservar instâncias para componentes estáveis, como o banco de dados.

## Backup e Recuperação

Automatizar backups de dados usando AWS Backup para EC2 e RDS.

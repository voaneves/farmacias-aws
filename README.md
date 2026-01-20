# RELATÓRIO DE IMPLEMENTAÇÃO E OTIMIZAÇÃO DE CUSTOS AWS

**Data:** 20/01/2026  
**Empresa:** Abstergo Industries  
**Responsável:** Victor Otávio Andrade das Neves  
**Departamento:** Escritório de Processos e Inovação

## 1. Introdução Executiva
Este documento detalha a implementação de soluções de arquitetura na nuvem AWS para a **Abstergo Industries**. O projeto, conduzido por **Victor Otávio Andrade das Neves**, teve como premissa a metodologia **FinOps** (Financial Operations), visando não apenas a redução imediata de custos operacionais (OpEx), mas também a instauração de uma cultura de eficiência no consumo de recursos computacionais.

## 2. Escopo e Objetivos
O objetivo central foi sanar ineficiências financeiras identificadas na infraestrutura atual. Foram selecionados 3 serviços nativos da AWS para atacar três pilares de desperdício:
1.  Falta de visibilidade de gastos.
2.  Capacidade ociosa de servidores.
3.  Armazenamento de dados frios em camadas caras.

## 3. Detalhamento da Implementação

### Etapa 1: Governança de Dados
- **Ferramenta:** AWS Cost Explorer
- **Foco:** Visibilidade, Auditoria e Rightsizing (Adequação de Tamanho).
- **Como reduz o custo:** - A ferramenta permitiu identificar recursos "zumbis" (ex: Load Balancers sem instâncias associadas e volumes EBS órfãos) que geravam cobrança sem entregar valor.
    - **Ação Prática:** Mapeamento de instâncias EC2 superdimensionadas (ex: uso de CPU abaixo de 5%), permitindo a troca por tipos de instância menores e mais baratos.

### Etapa 2: Elasticidade Computacional
- **Ferramenta:** Amazon EC2 Auto Scaling
- **Foco:** Eficiência Operacional e Pagamento sob Demanda.
- **Como reduz o custo:**
    - Substituição do modelo de provisionamento estático (servidores ligados 24/7 para suportar picos eventuais) pelo modelo dinâmico.
    - **Ação Prática:** Configuração de políticas de *Scale-In* (redução). Durante a madrugada e fins de semana, a frota de servidores é reduzida automaticamente para o mínimo viável, eliminando o custo de ociosidade.

### Etapa 3: Ciclo de Vida de Dados
- **Ferramenta:** Amazon S3 Intelligent-Tiering
- **Foco:** Otimização de Storage sem Overhead Operacional.
- **Como reduz o custo:**
    - O serviço monitora padrões de acesso e move objetos automaticamente entre camadas de acesso frequente (mais caras) e camadas de acesso infrequente ou arquivo (até 95% mais baratas).
    - **Ação Prática:** Aplicação da classe Intelligent-Tiering nos Buckets de Logs e Backups históricos, garantindo que dados não acessados há mais de 30 dias parem de cobrar a tarifa cheia de "S3 Standard".

## 4. Projeção de Impacto Financeiro
Com base na análise preliminar dos recursos, estimamos os seguintes resultados para o próximo trimestre (Q2):

| Área de Atuação | Ação Realizada | Redução Estimada (%) |
| :--- | :--- | :--- |
| **Computação (EC2)** | Eliminação de ociosidade via Auto Scaling | **30% a 40%** |
| **Armazenamento (S3)** | Migração automática para camadas frias | **20% a 25%** |
| **Recursos Órfãos** | Limpeza guiada pelo Cost Explorer | **10% (imediato)** |

## 5. Conclusão
A implementação das ferramentas na **Abstergo Industries** transformou a arquitetura de custos da empresa, migrando de um modelo de gasto fixo para um modelo variável otimizado. As ações descritas garantem que a empresa pague apenas pelo que efetivamente consome.

Recomenda-se a revisão mensal através do Cost Explorer para garantir que as políticas de Auto Scaling continuem alinhadas com a demanda de negócios.

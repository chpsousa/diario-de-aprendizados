
# Diário de aprendizados 

> Aqui eu registro de forma resumida os aprendizados, frases, lições, exemplos de código, tecnologias que aprendi e tive contato durante o dia a dia de trabalho.

📖

💻

😎

[Clique aqui](#conteúdos-separados-por-dia) para visualizar os conteúdos separados por dia.

## Conteúdos

- DevOps
    - [Pipeline do Azure DevOps com repositorio GitHub](#pipeline-do-azure-devops-com-repositorio-github)
- Padrões de projeto e Código Limpo
    - [Regra do Escoteiro](#regra-do-escoteiro)

## Conteúdos separados por dia

### 01/06/2020
    
#### Regra do escoteiro

>**Deixe o código mais limpo do que estava antes de você mexer nele**

A **regra do escoteiro** diz que um escoteiro sempre deve deixar o acampamento mais limpo do que encontrou.
Em uma conversa com [@vpteruel](https://github.com/vpteruel) e [@mvmjacobs](https://github.com/mvmjacobs), o [@mvmjacobs](https://github.com/mvmjacobs) comentou sobre a Regra do Escoteiro, no desenvolvimento. Desenvolvedores devem aplicar a regra no seu trabalho, onde todo código em que mexer, deve deixá-lo mais limpo do que encontrou.

Encontrei um [texto](https://becode.com.br/clean-code/#:~:text=Regra%20de%20Escoteiro&text=Para%20desenvolvedores%2C%20podemos%20adaptar%20para,n%C3%A3o%20impactar%20as%20funcionalidades%20existentes.) interessante no blog Be code que fala sobre isso

### 02/06/2020

#### Pipeline do Azure DevOps com repositorio GitHub

É possível realizar uma integração de seus repositórios do _GitHub_ e criar pipelines no _Azure DevOps_ que sejam ativados a partir de _pull requests_ criados no GitHub.

Para isso, abra seu [_Azure DevOps_](https://dev.azure.com/) e:
    - clique em seu projeto, na tela inicial do _Azure DevOps_
    - clique no menu _Pipelines_
    - clique em _new_
    - na opção _where is your code_, selecione _GitHub_
    - autentique com sua conta do _GitHub_

[Artigo de referência](https://docs.microsoft.com/en-us/azure/devops/pipelines/create-first-pipeline)
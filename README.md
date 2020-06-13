
# Diário de aprendizados 

> Aqui eu registro de forma resumida os aprendizados, frases, lições, exemplos de código, tecnologias que aprendi e tive contato durante o dia a dia de trabalho.

📖

💻

😎

[Clique aqui](#conteúdos-separados-por-dia) para visualizar os conteúdos separados por dia.

## Conteúdos

- .NET Core
    - [Adicionar Health Checks em uma API](#adicionar-health-checks-em-uma-api)
- C#
    - [Discards (-)](#discards)
- Code Review
- DevOps
    - [Pipeline do Azure DevOps com repositorio GitHub](#pipeline-do-azure-devops-com-repositorio-github)
    - [Badge do Azure Pipelines em repositório do GitHub](#badge-do-azure-pipelines-em-repositório-do-github)
    - [Gerar artefato para pipeline de release](#gerar-artefato-para-pipeline-de-release)
    - [Restore de pacotes NuGet em pipeline de deploy](#restore-de-pacotes-nuget-em-pipeline-de-deploy)
- Padrões de projeto e Código Limpo
    - [Regra do Escoteiro](#regra-do-escoteiro)
- Testes automatizados
    - [Testes com dependências externas]()

## Conteúdos separados por dia

### 01/06/2020
    
#### Regra do escoteiro

>**Deixe o código mais limpo do que estava antes de você mexer nele**

A **regra do escoteiro** diz que um escoteiro sempre deve deixar o acampamento mais limpo do que encontrou.
Em uma conversa com [@vpteruel](https://github.com/vpteruel) e [@mvmjacobs](https://github.com/mvmjacobs), o [@mvmjacobs](https://github.com/mvmjacobs) comentou sobre a Regra do Escoteiro, no desenvolvimento. Desenvolvedores devem aplicar a regra no seu trabalho, onde **todo código em que mexer, deve deixá-lo mais limpo do que encontrou**.

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

### 03/06/2020

#### Testes com dependências externas

Não se pode depender de um serviço externo em um teste de integração ou de unidade no qual você não tem controle.

Por exemplo:

Temos uma API que disponibiliza a temperatura de um equipamento. Uma aplicação se conecta nessa API para obter a temperatura do equipamento, e dependendo do valor da temperatura, define um comportamento esperado.

Os testes automatizados da aplicação não devem utilizar a chamada da API de temperaturas, pois caso ela esteja fora do ar, os testes não irão passar, e não teremos controle sobre isso, pois o código da API é externo. O que devemos testar, é se a chamada será realizada da forma correta.

O que podemos fazer então para resolver isso?

- Utilizar técnicas de _mocking_
- Criar serviços falsos para implementar o _mocking_

Em .NET, usando a biblioteca [FakeItEasy](https://fakeiteasy.github.io/) é possível criar instâncias _fakes_ das classes facilmente.
Com isso, se criarmos uma interface com assinaturas dos métodos que são utilizados para obter os valores, podemos criar um serviço verdadeiro para realizar as chamadas da API e um falso implementando a interface criada, e nos testes da aplicação podemos criar uma instância fake, para testar a chamada.

Também em .NET, podemos usar a biblioteca [MockHttp for HttpClient](https://github.com/richardszalay/mockhttp) e podemos criar um servidor http falso, podendo ser utilizado nos testes.

### 04/06/2020

#### Badge do Azure Pipelines em repositório do GitHub

Em repositórios do _GitHub_ que tiverem seus pipelines configurados no _Azure DevOps_ é possível colocar o badge do Azure Pipelines para sinalizar o _status_ de suas _builds_.

![Exemplo de um badge do Azure DevOps](https://docs.microsoft.com/en-us/azure/devops/pipelines/media/azure-pipelines-succeeded.png?view=azure-devops)

Para colocar o _badge_ siga os passos:
    - clique no pipeline que deseja
    - clique na opção "..."
    - clique no menu _status badge_
    - copie o valor informado
    - cole no seu README.md

[Artigo de referência](https://docs.microsoft.com/en-us/azure/devops/pipelines/media/azure-pipelines-succeeded.png?view=azure-devops)

### 04/06/2020

#### Gerar artefato para pipeline de release

o pipeline de build de uma aplicação no _Azure DevOps_ deve gerar um artefato para o pipeline de release.
Para isso, em aplicações .NET Core, existe uma task para gerar o artefato:

```
- task: PublishBuildArtifacts@1
  inputs:
    pathtoPublish: '$(Build.ArtifactStagingDirectory)' 
    artifactName: 'your-artifact-name'
```


### 05/06/2020

#### Discards

A partir do C# 7.0 foram criados os _discards_, que são variáveis temporárias que não são usadas em seu código.
Elas não possuem valor, e não possuem memória alocada e nem espaço de armazenamento.
Para indicar um _discard_ basta usar um "_" como o nome da variável.

Alguns exemplos:

```
var pessoa = new Pessoa("Carlos", "Henrique", "São Paulo", "SP", "Brasil");
var (primeiroNome, _, cidade, _, _) = pessoa;
Console.WriteLine($"Olá {primeiroNome} de {cidade}!");
```
```
objeto switch
{
    Tipo1 _ => _servicoTipo1,
    Tipo2 _ => _servicoTipo2,
    Tipo3 _ => _servicoTipo3,
    _ => throw new InvalidOperationException(
        $"Tipo inválido")
};
```

[Artigo de referência](https://docs.microsoft.com/en-us/dotnet/csharp/discards)


#### Restore de pacotes NuGet em pipeline de deploy

Nos _pipelines_ de _build_ do _Azure DevOps_, quando seu projeto utiliza pacotes NuGet de um _feed_ externo, você pode usar uma task específica para realizar o restore:

```
 - task: NuGetCommand@2
 inputs:
 command: 'restore'
 restoreSolution: '**/*.sln'
 feedsToUse: 'select'
 vstsFeed: 'chave-do-feed'
```
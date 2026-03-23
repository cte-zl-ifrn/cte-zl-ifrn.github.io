# SUAP Edu - Diários

## Digrama

```mermaid
classDiagram
    class Diario{
        _: VerDiagramaDiarios
    }
    class ConfiguracaoAvaliacao{
        diario: Diario
        etapa: Integer
        forma_calculo: Integer!
        divisor: Integer
        maior_nota: Boolean!
        menor_nota: Boolean!
        autopublicar: Boolean!
        observacao: String
    }
    class ItemConfiguracaoAvaliacao{
        configuracao_avaliacao: ConfiguracaoAvaliacao!
        tipo: int!
        sigla: String
        descricao: String!
        data: Date
        nota_maxima: int
        peso: int
    }
    class MatriculaDiario {
        _: VerDiagramaHistorico
    }
    class NotaAvaliacao{
        matricula_diario: MatriculaDiario!
        item_configuracao_avaliacao: ItemConfiguracaoAvaliacao!
        nota: Nota
    }
    MatriculaDiario "1" <-- "n" NotaAvaliacao 
    Diario "1" <-- "n" ConfiguracaoAvaliacao
    ConfiguracaoAvaliacao "1" <-- "n" ItemConfiguracaoAvaliacao
    ItemConfiguracaoAvaliacao "1" <-- "n" NotaAvaliacao
```


## Choices

> **ConfiguracaoAvaliacao**
> 1. tipo=[[1, 'Soma Simples'], [2, 'Média Aritmética'], [3, 'Média Ponderada'], [4, 'Maior Nota'], [5, 'Soma com Divisor Informado'], [6, 'Média Atitudinal'], [7, 'Avaliação por Conceito']]

> **ItemConfiguracaoAvaliacao**
> 1. tipo=`[[1, 'Trabalho'], [2, 'Seminário'], [3, 'Teste'], [4, 'Prova'], [5, 'Atividade'],  [6, 'Exercício'], [7, 'Atitudinal']]`

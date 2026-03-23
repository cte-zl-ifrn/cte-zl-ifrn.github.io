# SUAP Edu

## Componente - Digrama

```mermaid
classDiagram
    class NivelEnsino {
        descricao: String!!
    }
    class TipoComponente{
        descricao: String!
    }
    class GrupoAtuacao{
        descricao: String!        
    }
    class Componente {
        descricao: String!
        descricao_historico: String!
        tipo: TipoComponente!
        sigla: String!!
        diretoria: Diretoria!
        nivel_ensino: NivelEnsino!
        ativo: Boolean!

        ch_hora_relogio: Integer!
        ch_hora_aula: Integer!
        ch_qtd_creditos: Integer!

        observacao: Text
        sigla_qacademico: String
        abreviatura: String

        grupo_atuacao: GrupoAtuacao

        sequencial: Integer
    }
    class ClassificacaoComplementarComponenteCurricular {
        descricao: String!!
    }
    class Nucleo{
        descricao: String!!
    }
    class ComponenteCurricular {
        %% Dados gerais
        matriz: Matriz!
        componente: Componente!
        classificacao_complementar: ClassificacaoComplementarComponenteCurricular
        periodo_letivo: Integer!
        tipo: IntegerChoice
        optativo: Boolean!
        is_seminario_estagio_docente: Boolean!
        tipo_estagio_docente: IntegerChoice
        tipo_modulo: IntegerChoice
        qtd_avaliacoes: IntegerChoice
        nucleo: Nucleo!

        %% Carga horária
        ch_presencial: Integer!
        ch_pratica: Integer!
        ch_extensao: Integer!
        ch_pcc: Integer!
        ch_visita_tecnica: Integer!
        percentual_maximo_ead: Integer!
        qtd_aulas_ead: Integer!

        %% Pré requisitos
        pre_requisitos: Many(ComponenteCurricular)

        %% Co-requisitos
        co_requisitos: Many(ComponenteCurricular)

        avaliacao_por_conceito: Boolean!
        is_dinamico: Boolean!
        componente_curricular_associado: ComponenteCurricular
        segundo_semestre: Boolean!
        pode_fechar_pendencia: Boolean!
        ementa: Text

        %% distribuição da quantidade de créditos do componente curricular anual no semestre
        ch_semanal_1s: Integer
        ch_semanal_2s: Integer
    }


    class Matriz{
        _: VerDiagramaMatriz
    }

    class Diario{
        _: VerDiagramaDiario
    }

    Componente "N" --> "1" TipoComponente
    Componente "N" --> "1" NivelEnsino
    Componente "N" --> "1" GrupoAtuacao
    Componente "N" --> "1" Diretoria

    ComponenteCurricular "N" --> "1" Matriz
    ComponenteCurricular "N" --> "1" Componente
    ComponenteCurricular "N" --> "1" ClassificacaoComplementarComponenteCurricular
    ComponenteCurricular "N" --> "1" Nucleo

    Diario "N" --> "1" ComponenteCurricular
```

> **ComponenteCurricular**
> 1. tipo = `[[1, 'Regular'], [2, 'Seminário'], [3, 'Prática Profissional'], [4, 'Trabalho de Conclusão de Curso'], [5, 'Atividade de Extensão'], [6, 'Prática como Componente Curricular'], [7, 'Visita Técnica / Aula da Campo'], [8, 'Componentes Extracurriculares']]`
> 2. tipo_estagio_docente = `[[1, 'Estágio Docente I'], [2, 'Estágio Docente II'], [3, 'Estágio Docente III'], [4, 'Estágio Docente IV'], [5, 'Estágio Docente de Matriz Anterior']]`
> 3. tipo_modulo = `[[1, 'Módulo I'], [2, 'Módulo II'], [3, 'Módulo III'], [4, 'Módulo IV'], [5, 'Módulo V'], [6, 'Módulo VI'], [7, 'Módulo VII'], [8, 'Módulo VIII'], [9, 'Módulo IX'], [10, 'Módulo X'], [11, 'Módulo XI'], [12, 'Módulo XII']]`
> 4. qtd_avaliacoes = `[[0, 'Zero'], [1, 'Uma'], [2, 'Duas'], [3, 'Três'], [4, 'Quatro']]`
# SUAP Edu

## Componente - Digrama

```mermaid
classDiagram
    class NaturezaParticipacao {
        descricao: String!!
    } 
    class NivelEnsino {
        descricao: String!!
    }
    class Matriz {
        %% Dados gerais
        descricao: String
        ano_criacao: Integer
        periodo_criacao: Integer [[1, '1'], [2, '2']]
        ativo: Boolean
        data_inicio: Date
        data_fim: Date 
        ppp: File 
        ppc: File 
        qtd_periodos_letivos: Integer [[x, x] for x in range(1, 13)])
        nivel_ensino: NivelEnsino 
        natureza_participacao: NaturezaParticipacao 

        %% Carga horária
        ch_componentes_obrigatorios: Integer
        ch_componentes_optativos: Integer
        ch_componentes_eletivos: Integer
        ch_seminarios: Integer
        ch_pratica_profissional: Integer
        ch_atividades_complementares: Integer
        ch_atividades_aprofundamento: Integer
        ch_componentes_extensao: Integer
        ch_componentes_tcc: Integer
        ch_pratica_como_componente: Integer
        ch_visita_tecnica: Integer
        ch_atividades_extensao: Integer
        ch_componentes_com_extensao: Integer

        componentes: Many(ComponenteCurricular)

        inconsistente: Boolean
        exige_tcc: Boolean
        permite_etapas_componente_tcc: Boolean

        observacao: Text 

        %% Estágio
        exige_estagio: Boolean 
        ch_minima_estagio: Integer 
        periodo_minimo_estagio_obrigatorio: IntegerChoice
        periodo_minimo_estagio_nao_obrigatorio: IntegerChoice

        requer_vinculacao_extensao_diarios: Boolean!

        %% certificação parcial
        emite_certificacao_parcial: Boolean!
        certificado_parcial_acumulavel: Boolean!
    }
    class CursoTecnico{
        _: VerDiagramaCurso
    }
    class CursoCampus{
        _: VerDiagramaCurso
    }
    class ComponenteCurricular {
        _: VerDiagramaComponente
        matriz: Matriz!
    }
    class MatrizCurso {
        curso_campus: CursoCampus!
        matriz: Matriz!
        resolucao_criacao: Text
        resolucao_data: Date
        reconhecimento_texto: Text
        reconhecimento_data: Date
        unique_together = [('matriz', 'curso_campus')]
    }
    class RotuloModulo {
        matriz: Matriz
        descricao: String!
        tipo_modulo: IntegerChoice!

        unique_together = [('matriz', 'tipo_modulo')]
    }
    class Turma {
        _: VerDiagramaTurma
    }

    Matriz "n" --> "1" NivelEnsino
    Matriz "n" --> "1" NaturezaParticipacao

    Matriz "n" --> "n" Curso

    MatrizCurso "n" --> "1" Curso
    MatrizCurso  "n" --> "1" Matriz

    ComponenteCurricular "n" --> "1" Matriz

    RotuloModulo "n" --> "1" Matriz

    Turma "n" --> "1" Matriz
```

> **Matriz**
> 1. periodo_minimo_estagio_obrigatorio=`[['', '------']] + [[x, x] for x in range(1, 11)]`
> 2. periodo_minimo_estagio_nao_obrigatorio= `[['', '------']] + [[x, x] for x in range(1, 11)]`


> **RotuloModulo**
> 1. tipo_modulo=`[[1, 'Módulo I'], [2, 'Módulo II'], [3, 'Módulo III'], [4, 'Módulo IV'], [5, 'Módulo V'], [6, 'Módulo VI'], [7, 'Módulo VII'], [8, 'Módulo VIII'], [9, 'Módulo IX'], [10, 'Módulo X'], [11, 'Módulo XI'], [12, 'Módulo XII']]`

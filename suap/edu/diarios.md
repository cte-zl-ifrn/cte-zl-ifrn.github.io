# SUAP Edu - Diários

## Digrama

```mermaid
classDiagram
    class ComponenteCurricular {
        _: VerDiagramaComponentes
    }
    class CursoCampus {
        _: VerDiagramaCursos
        modalidade: Modalidade
        area: AreaCurso
        eixo: EixoTecnologico
        curso_tecnico: CursoTecnico
        area_capes: AreaCapes
        area_curso_formacao_superior: AreaCursoFormacaoSuperior
        justificativa_dispensa_ingressante: JustificativaDispensaEnade
        area_concentracao: AreaConcentracao
        diretoria: Diretoria
        coordenador: IfrnId 🥸
        coordenador_2: IfrnId 🥸
        matrizes: Matriz
        mesmo_curso: CursoCampus
    }
    class Turma{
        _: VerDiagramaTurma
    }
    class Diario{
        turma: Turma!
        componente_curricular: ComponenteCurricular!
        percentual_minimo_ch: PositiveInteger!
        ano_letivo: int!
        periodo_letivo: int!
        quantidade_vagas: int!
        situacao: int!
        horario_campus: HorarioCampus!
        turno: Turno!
        estrutura_curso: EstruturaCurso!
        calendario_academico: CalendarioAcademico!
        local_aula: Sala
        local_laboratorio: Sala
        locais_aula_secundarios: set[Sala]
        descricao_dinamica: String
        segundo_semestre: Boolean!
        integracao_com_moodle: Boolean!
        url_moodle: String
        url_ambiente_virtual: String
        ignorar_choque_horario_renovacao_matricula: BooleanField!
        posse_etapa_1: int!
        posse_etapa_2: int!
        posse_etapa_3: int!
        posse_etapa_4: int!
        posse_etapa_5: int!
        entregue_fisicamente: Boolean
        possui_segunda_oferta: Boolean!
        diario_primeira_oferta: Diario
    }
    class ProfessorDiario{
        diario: Diario!
        professor: IfrnId! 🥸
        tipo: TipoProfessorDiario!
        data_inicio_etapa_1: Date
        data_fim_etapa_1: Date
        data_inicio_etapa_2: Date
        data_fim_etapa_2: Date
        data_inicio_etapa_3: Date
        data_fim_etapa_3: Date
        data_inicio_etapa_4: Date
        data_fim_etapa_4: Date
        data_inicio_etapa_final: Date
        data_fim_etapa_final: Date
        ativo: Boolean!
        financiamento_externo: Boolean!
        percentual_ch: Integer
        periodo_letivo_ch: Integer
    }
    class TipoProfessorDiario {
        descricao: String!!
    }
    class Aula {
        professor_diario: ProfessorDiario!
        etapa: Integer!
        quantidade: Integer!
        url: String
        data: Date
        conteudo: TextField
        tipo: Integer
        ead: Boolean!
        outros_professor_diario: Many(ProfessorDiario)
        registro_frequencia_confirmado: Boolean!
    }

    Turma "1" <-- "n" Diario
    CursoCampus "1" <-- "n" Turma
    ComponenteCurricular "1" <-- "n" Diario

    Diario "n" --> "1" Sala: local_aula
    Diario "n" --> "1" Sala: local_laboratorio
    Diario "n" --> "1" Sala: locais_aula_secundarios
    
    %% Diario -- Turno
    %% Diario -- HorarioCampus
    %% Diario -- EstruturaCurso
    %% Diario -- CalendarioAcademico

    ProfessorDiario --> Diario
    ProfessorDiario --> TipoProfessorDiario

    Aula --> ProfessorDiario
```


## Choices
> **Diario**
> 1. situacao=`[[1, 'Aberto'], [2, 'Fechado']]`
> 2. posse_etapa_1, posse_etapa_2, posse_etapa_3, posse_etapa_4, posse_etapa_5=`[[1, 'Professor'], [0, 'Registro Escolar']]`
> 3. etapa=`[[1, 'Etapa 1'], [2, 'Etapa 2'], [3, 'Etapa 3'], [4, 'Etapa 4'], [5, 'Etapa Final']]`

> **Aula**
> 1. etapa=`[[1, 'Primeira'], [2, 'Segunda'], [3, 'Terceira'], [4, 'Quarta'], [5, 'Final']]`
> 2. tipo=`[[1, 'Teórica'], [2, 'Prática'], [3, 'Extensão'], [4, 'Prática como Componente Curricular'], [5, 'Visita Técnica/Aula de Campo']]`


## Observações

1. Os models abaixo não foram utilizados pois não pareceram ter relevância para a integração:
   1. `edu.diarios.ObservacaoDiario`
   1. `edu.diarios.OcorrenciaDiario`
   1. `edu.diarios.MaterialAula`
   1. `edu.diarios.MaterialDiario`
   1. `edu.diarios.Trabalho`
   1. `edu.diarios.EntregaTrabalho`
   1. `edu.diarios.TopicoDiscussao`
   1. `edu.diarios.RespostaDiscussao`
   1. `edu.diarios.JustificativaSuspensaoDiario`
   1. `edu.diarios.SuspensaoDiario`

# SUAP Edu - Diários

## Digrama

```mermaid
classDiagram
    class Componente {
        descricao: String!
        descricao_historico: String!
        tipo: TipoComponente!
        sigla: String!!
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
        pre_requisitos: "1" --> "0..*" ComponenteCurricular

        %% Co-requisitos
        co_requisitos: "1" --> "0..*" ComponenteCurricular

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
    class ClassificacaoComplementarComponenteCurricular {
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

        componentes: Many[Componente(ComponenteCurricular)]

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
        codigo_inep: String!!
        nome: String!!
        eixo_tecnologico: EixoTecnologico!
        excluido: Boolean!
    }
    class CursoCampus{
        %% Identificação
        codigo_academico: Integer
        descricao: String!
        descricao_historico: String!
        codigo_censup: String
        codigo_emec: String
        codigo_sistec: String
        codigo_educacenso: String
        ciencia_sem_fronteira: Boolean!
        formacao_de_professores: Boolean!

        %% Dados da funcionamento
        data_inicio: Date
        data_funcionamento: Date
        ano_letivo: Integer
        periodo_letivo: Integer
        ativo: Boolean!

        %% Outros Dados
        data_fim: Date
        data_solicitacao_reconhecimento: Date
        data_limite_reconhecimento: Date
        suspenso: Boolean!
        em_extincao: Boolean!
        extinto: Boolean!

        codigo: String!!
        modalidade: Modalidade
        plano_ensino: Boolean!
        quantidade_vagas: Integer

        %% cursos Licenciatura
        area: AreaCurso
        coordenadores_estagio_docente: "1" --> "0..*" IfrnId
        %% cursos tecnológicos ou FIC
        eixo: EixoTecnologico

        %% cursos técnicos concomitantes e subsequentes
        curso_tecnico: CursoTecnico

        %% cursos de pós-graduação
        area_capes: AreaCapes

        area_curso_formacao_superior: AreaCursoFormacaoSuperior

        exige_enade: Boolean!
        justificativa_dispensa_ingressante: JustificativaDispensaEnade 
        processamento_enade: Boolean!

        periodicidade: StringChoice
        exige_colacao_grau: Boolean!
        assinatura_digital: Boolean!
        emite_diploma: Boolean!
        assinatura_eletronica: Boolean!
        area_concentracao: AreaConcentracao
        programa: String
        diretoria: Diretoria
        extensao: Boolean
        coordenador: IfrnId
        numero_portaria_coordenador: String
        coordenador_2: IfrnId
        numero_portaria_coordenador_2: String
        matrizes: "1" --> "0..*" Matriz
        mesmo_curso: CursoCampus

        %% Titulo do certificado de conclusão
        titulo_certificado_masculino: String
        titulo_certificado_feminino: String

        %% Atributo de Minicurso
        ppc: File 
        ch_total: Integer
        ch_aula: Integer
        tipo_hora_aula: StringChoice
        resolucao_criacao: Text

        fator_esforco_curso: Decimal(4, 2)

        %% Autoinstrucional
        autoinstrucional: Boolean

    }

    class MatrizCurso {
        curso_campus: CursoCampus!
        matriz: Matriz!

        %% Ato normativo
        resolucao_criacao: Text
        resolucao_data: Date
        %% Ato de reconhecimento
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
    class Minicurso {
    }
    class ConteudoMinicurso {
        descricao: String!
        ch: Integer!
        minicurso: Minicurso!
    }
    class Modalidade {
        descricao: String!!
        nivel_ensino: NivelEnsino
    }
    class AreaCurso {
        descricao: String!!
    }
    class EixoTecnologico {
        descricao: String!!
        codigo_inep: String
    }
    class NivelEnsino {
        descricao: String!!
    }
    class IfrnId {
        tipo_relacionamento: IntegerChoice
        ativo: Boolean!
        username: String!!
        first_name: String!
        last_name: String!
        email: String!
        is_active: Boolean
        eh_servidor: Boolean!
        eh_aluno: Boolean!
        eh_prestador: Boolean!
        eh_usuarioexterno: Boolean!
        eh_docente: Boolean!
        eh_tecnico_administrativo: Boolean!
        eh_estrangeiro: Boolean!
        nome: String!
        nome_usual: String!
        nome_social: String
        nome_registro: String
        email: Email
        email_secundario: Email!
    }
    class TipoComponente{
        descricao: String!
    }
    class NaturezaParticipacao {
        descricao: String!!
    } 
    class Nucleo{
        descricao: String!!
    }
    class Turma{
        codigo: String!
        descricao: String!
        ano_letivo: int!
        periodo_letivo: int!
        periodo_matriz: int!
        turno: Turno
        curso_campus: CursoCampus
        matriz: Matriz
        polo: Polo
        convenio: Convenio
        sigla: String
        codigo_educacenso: String
    }
    class TurmaMinicurso{
        descricao: String!
        turno: Turno
        ano_letivo: Integer!
        periodo_letivo: Integer!
        data_inicio: Date!
        data_fim: Date!
        minicurso: Minicurso!
        gerar_matricula: Boolean!
        modelo_padrao: Boolean!
        nota_minima: Integer!
        completude_minima: Integer
        integracao_com_moodle: Boolean
        url_moodle: String
        url_ambiente_virtual: String
    }
    class Convneio{
        descricao: String!!
    }
    class Polo{
        descricao: String!
        sigla: String!
    }
    class ParticipanteTurmaMinicurso{
        aluno: Aluno!
        turma: TurmaMinicurso!
        nota: Integer
        completude: Integer
    }
    class MonitorMinicurso{
        aluno: Aluno!
        turma_minicurso: TurmaMinicurso!
        carga_horaria: Integer
    }
    class ProfessorMinicurso{
        professor: IfrnId!
        turma_minicurso: TurmaMinicurso!
        carga_horaria: Integer
        carga_horaria_semanal: Decimal
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
        locais_aula_secundarios: ManySala
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
        professor: IfrnId!
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
    class TipoProfessorDiario{
        descricao: String!!
    }
    class Aula{
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
    class Falta{
        matricula_diario: MatriculaDiario!
        aula: Aula!
        quantidade: Integer!
        abono_faltas: AbonoFaltas
        contabilizar: Boolean!
    }

    Componente --> TipoComponente
    Componente --> NivelEnsino
    Componente --> GrupoAtuacao

    ComponenteCurricular --> Matriz
    ComponenteCurricular --> Componente
    ComponenteCurricular --> ClassificacaoComplementarComponenteCurricular
    ComponenteCurricular --> Nucleo

    CursoCampus --> Modalidade
    CursoCampus --> AreaCurso
    CursoCampus --> EixoTecnologico
    CursoCampus --> CursoTecnico
    CursoCampus --> IfrnId

    Matriz --> NivelEnsino
    Matriz --> NaturezaParticipacao
    Matriz --> Componente
    
    MatrizCurso --> Curso
    MatrizCurso --> Matriz

    RotuloModulo --> Matriz

    Minicurso --|> Curso

    ConteudoMinicurso --> Minicurso

    Turma --> Turno
    Turma --> CursoCampus
    Turma --> Polo
    Turma --> Convenio
    Turma --> Matriz

    TurmaMinicurso --> Turno
    TurmaMinicurso --> Minicurso

    ParticipanteTurmaMinicurso --> Aluno
    ParticipanteTurmaMinicurso --> TurmaMinicurso

    MonitorMinicurso --> Aluno
    MonitorMinicurso --> TurmaMinicurso

    ProfessorMinicurso --> IfrnId
    ProfessorMinicurso --> TurmaMinicurso

    Diario --> Turma
    Diario --> ComponenteCurricular
    Diario --> HorarioCampus
    Diario --> Turno
    Diario --> EstruturaCurso
    Diario --> CalendarioAcademico
    Diario --> Sala

    ProfessorDiario --> Diario
    ProfessorDiario --> Professor
    ProfessorDiario --> TipoProfessorDiario

    Falta --> MatriculaDiario
    Falta --> Aula
    Falta --> AbonoFaltas

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

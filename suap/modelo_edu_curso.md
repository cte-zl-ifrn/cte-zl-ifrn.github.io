# SUAP Edu

## Curso - Digrama

```mermaid
classDiagram
    class Componente {
        _: VerDiagramaComponente
    }
    class ComponenteCurricular {
        _: VerDiagramaComponente
        matriz: Matriz!
        componente: Componente!
        componente_curricular_associado: ComponenteCurricular
    }
    class Matriz {
        _: VerDiagramaMatriz
        nivel_ensino: NivelEnsino
        componentes: set[ComponenteCurricular]
    }

    class EixoTecnologico {
        descricao: String!!
        codigo_inep: String
    }
    class CursoTecnico{
        codigo_inep: String!!
        nome: String!!
        eixo_tecnologico: EixoTecnologico!
        excluido: Boolean!
    }
    class Modalidade {
        descricao: String!!
        nivel_ensino: NivelEnsino
    }
    class EixoTecnologico {
        descricao: String!!
        codigo_inep: String
    }
    class AreaCapes {
        descricao: String!!
    }
    class AreaCursoFormacaoSuperior {
        codigo_cine: String!
        codigo_area_detalhada: String!
        codigo_area_especifica: String!
        codigo_area_geral: String!

        cine: String
        area_detalhada: String!
        area_especifica: String!
        area_geral: String!
    }

    class JustificativaDispensaENADE{
        descricao: String!!
        ativo: Boolean!
    }
    class AreaConcentracao{
        descricao: String!!
        area_capes: AreaCapes
        area_avaliacao: AreaAvaliacao
    }
    class Diretoria{
        _: VerDiagramaDiretoria
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
        coordenadores_estagio_docente: set[IfrnId]
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

        periodicidade: String
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
        tipo_hora_aula: String
        resolucao_criacao: Text

        fator_esforco_curso: Decimal(4, 2)

        %% Autoinstrucional
        autoinstrucional: Boolean

    }
    class MatrizCurso {
        _: VerDiagramaMatriz
    }
    class Minicurso {
    }
    class ConteudoMinicurso {
        descricao: String!
        ch: Integer!
        minicurso: Minicurso!
    }
    class AreaCurso {
        descricao: String!!
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

    Componente --> NivelEnsino
    Componente --> GrupoAtuacao

    ComponenteCurricular --> Matriz
    ComponenteCurricular --> Componente

    CursoCampus --> Modalidade
    CursoCampus --> AreaCurso
    CursoCampus --> EixoTecnologico
    CursoCampus --> CursoTecnico
    CursoCampus --> IfrnId

    CursoCampus "n" --> "1" Diretoria

    Matriz --> NivelEnsino
    Matriz --> Componente
    
    MatrizCurso --> Curso
    MatrizCurso --> Matriz

    RotuloModulo --> Matriz

    Minicurso --|> Curso

    ConteudoMinicurso --> Minicurso
```


> **Curso**
> 1. periodo_letivo= `[[1, '1'], [2, '2']]`
> 2. periodicidade= `[[1, 'Anual'], [2, 'Semestral'], [3, 'Livre']]`
> 3. tipo_hora_aula= `[[45, '45 min'], [60, '60 min']]`
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
        matrizes: set[Matriz]
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
        _: VerDiagramaIfrnId
    }

    Componente "n" --> "1" NivelEnsino
    Componente "n" --> "1" GrupoAtuacao

    ComponenteCurricular "n" --> "1" Matriz
    ComponenteCurricular "n" --> "1" Componente
    ComponenteCurricular "n" --> "1" Matriz

    CursoCampus "n" --> "1" Modalidade
    CursoCampus "n" --> "1" AreaCurso
    CursoCampus "n" --> "1" AreaCapes
    CursoCampus "n" --> "1" EixoTecnologico
    CursoCampus "n" --> "1" CursoTecnico
    CursoCampus "n" --> "1" IfrnId : coordenador
    CursoCampus "n" --> "1" IfrnId : coordenador_2
    CursoCampus "n" --> "n" IfrnId : coordenadores_estagio_docente
    CursoCampus "n" --> "1" AreaConcentracao
    CursoCampus "n" --> "1" Diretoria
    CursoCampus "n" --> "1" AreaCursoFormacaoSuperior
    CursoCampus "n" --> "1" JustificativaDispensaEnade

    CursoTecnico "n" --> "1" EixoTecnologico

    Matriz "n" --> "1" NivelEnsino
    
    MatrizCurso "n" --> "1" CursoCampus
    MatrizCurso "n" --> "1" Matriz

    Minicurso --|> CursoCampus

    ConteudoMinicurso "n" --> "1" Minicurso
```


> **Curso**
> 1. periodo_letivo= `[[1, '1'], [2, '2']]`
> 2. periodicidade= `[[1, 'Anual'], [2, 'Semestral'], [3, 'Livre']]`
> 3. tipo_hora_aula= `[[45, '45 min'], [60, '60 min']]`


## Observações

1. Os models abaixo não foram utilizados pois não pareceram ter relevância para a integração:
   1. `edu.cursos.EstruturaCurso`
   2. `edu.cursos.Habilitacao`
   3. `edu.cursos.RepresentacaoConceitual`
   4. `edu.cursos.EquivalenciaComponenteQAcademico`
   5. `edu.cursos.Autorizacao`
   6. `edu.cursos.Reconhecimento`
   7. `edu.cursos.ConfiguracaoCertificacaoParcial`
   8. `edu.cursos.ComponenteCurricularCertificacaoParcial`

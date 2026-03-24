# SUAP Edu

## Turma - Digrama

```mermaid
classDiagram
    class CursoCampus {
        _: VerDiagramaCurso
    }
    class IfrnId {
        _: VerDiagramaIfrnId
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
    class Minicurso {
    }
    class ParticipanteTurmaMinicurso {
        aluno: Aluno!
        turma: TurmaMinicurso!
        nota: Integer
        completude: Integer
    }
    class MonitorMinicurso {
        aluno: Aluno!
        turma_minicurso: TurmaMinicurso!
        carga_horaria: Integer
    }
    class ProfessorMinicurso {
        professor: Professor!
        turma_minicurso: TurmaMinicurso!
        carga_horaria: Integer
        carga_horaria_semanal: Decimal
    }

    Turma  "n" --> "1" CursoCampus

    CursoCampus <|-- Minicurso

    TurmaMinicurso "n" --> "1" Minicurso
    TurmaMinicurso "1" <-- "n" ParticipanteTurmaMinicurso
    ParticipanteTurmaMinicurso "n" <-- "1" IfrnId: aluno
    TurmaMinicurso "1" <-- "n" MonitorMinicurso
    MonitorMinicurso "n" <-- "1" IfrnId : aluno
    TurmaMinicurso "1" <-- "n" ProfessorMinicurso
    ProfessorMinicurso "1" <-- "n" IfrnId : professor

```


## Observações

1. Os models abaixo não foram utilizados pois não pareceram ter relevância para a integração:
   1. `edu.cadastros_gerais.Turno`
   2. `edu.cadastros_gerais.Convenio`
   3. `edu.polos.Polo`

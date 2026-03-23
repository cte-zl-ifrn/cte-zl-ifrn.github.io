# SUAP Edu

## Curso - Digrama

```mermaid
classDiagram
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

    class Turno{
        descricao: String!!
        codigo_enade: String
    }
    class CursoCampus {
        _: VerDiagramaCurso
    }
    class Matriz {
        _: VerDiagramaMatriz
    }
    class Polo {
        _: VerDiagramaPolo
    }
    class Convenio{
        descricao: String!!
    }

    class Minicurso {
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

    Turma "n" --> "1" Polo
    Turma  "n" --> "1" Convenio
    Turma  "n" --> "1" CursoCampus
    Turma "n" --> "1" Matriz
    Turma "n" --> "1" Turno

    CursoCampus <|-- Minicurso
    CursoCampus "n" <-- "n "Matriz

    TurmaMinicurso "n" --> "1" Turno
    TurmaMinicurso "n" --> "1" Minicurso


```
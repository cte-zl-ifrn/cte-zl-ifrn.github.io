# SUAP Edu

## Curso - Digrama

```mermaid
classDiagram
    class IfrnId {
        _: VerDiagramaIfrnId
    }
    class UnidadeOrganizacional {
        _: VerDiagramaRh
    }
    class Diretoria {
        _: VerDiagramCadastroGerais
    }
    class Cidade {
        _: VerDiagramCadastroGerais
    }
    class CursoCampus {
        _: VerDiagramaCursos
    }
    class Sala {
        _: VerDiagramCadastroGerais
    }
    class Polo {
        cidade: Cidade
        diretoria: Diretoria
        campus_atendimento: UnidadeOrganizacional
        descricao: String!
        sigla: String!
        codigo_academico: Integer
        codigo_censup: String!
        estrutura_disponivel: String
        logradouro: String
        numero: String
        complemento: String
        bairro: String
        cep: String
        do_municipio: Boolean!
        telefone_principal: String
        telefone_secundario: String
    }
    class CoordenadorPolo {
        polo: Polo!
        vinculo: Vinculo!
        titular: Boolean!
    }
    class TutorPolo {
        polo: Polo!
        vinculo: Vinculo!
        cursos: set[CursoCampus]
    }
    class AtividadePolo {
        polo: Polo!
        user: User!
        nome: String
        descricao: String
        sala: Sala
        data_inicio: DateTime!
        data_fim: DateTime!
        confirmada: Boolean!
    }
    class Turno {
        descricao: String!!
        codigo_enade: String
    }
    class HorarioFuncionamentoPolo {
        polo: Polo!
        turno: Turno!
        numero: Integer!
        inicio: String!
        termino: String!
    }
    class HorarioPolo {
        polo: Polo!
        horario_funcionamento: HorarioFuncionamentoPolo!
        dia_semana: Integer!
    }
    class HorarioTutorPolo {
        tutor: TutorPolo!
        dia_semana: Integer!
        horario_funcionamento: HorarioFuncionamentoPolo!
    }
    class HorarioCoordenadorPolo {
        coordenador: CoordenadorPolo!
        dia_semana: Integer!
        horario_funcionamento: HorarioFuncionamentoPolo!
    }

    Cidade "1" <-- "n" Polo
    Diretoria "1" <-- "n" Polo
    UnidadeOrganizacional "1" <-- "n" Polo

    Polo "1" --> "n" CoordenadorPolo
    Polo "1" --> "n" TutorPolo
    Polo "1" --> "n" AtividadePolo
    Polo "1" --> "n" HorarioFuncionamentoPolo
    Polo "1" --> "n" HorarioPolo

    CoordenadorPolo "n" <-- "1" IfrnId
    TutorPolo "n" <-- "1" IfrnId
    TutorPolo "n" -- "n" CursoCampus

    AtividadePolo "n" <-- "1" IfrnId
    AtividadePolo "n" <-- "1" Sala
    
    HorarioFuncionamentoPolo "n" <-- "1" Turno
    HorarioFuncionamentoPolo "1" <-- "n" HorarioPolo
    HorarioFuncionamentoPolo "1" <-- "n" HorarioTutorPolo
    HorarioFuncionamentoPolo "1" <-- "n" HorarioCoordenadorPolo
```

> **HorarioPolo**, **HorarioCoordenadorPolo** e **HorarioTutorPolo**
> 1. dia_semana=`[[1, 'Segunda'], [2, 'Terça'], [3, 'Quarta'], [4, 'Quinta'], [5, 'Sexta'], [6, 'Sábado'], [7, 'Domingo']]`

> **HorarioFuncionamentoPolo**
> 1. numero=`[[1, '1'], [2, '2'], [3, '3'], [4, '4'], [5, '5'], [6, '6']]`
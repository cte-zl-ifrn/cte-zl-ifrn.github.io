# SUAP Edu

## Curso - Digrama

```mermaid
classDiagram
    class Polo {
        descricao: String!
        sigla: String!
        cidade: Cidade
        codigo_academico: Integer
        codigo_censup: String!
        estrutura_disponivel: String
        logradouro: String
        numero: String
        complemento: String
        bairro: String
        cep: String
        do_municipio: Boolean!
        diretoria: Diretoria
        telefone_principal: Stringl
        telefone_secundario: String
        campus_atendimento: UnidadeOrganizacional
    }
    class AtividadePolo {
        polo: Polo!
        nome: String
        descricao: String
        sala: Sala
        data_inicio: DateTime!
        data_fim: DateTime!
        user: User!
        confirmada: Boolean!
    }
    class IfrnId {
        _: VerDiagramaIfrnId
    }
    class HorarioFuncionamentoPolo {
        polo: Polo!
        numero: Integer!
        turno: Turno!
        inicio: String!
        termino: String!
    }
    class TutorPolo {
        polo: Polo!
        vinculo: Vinculo!
        cursos: set[CursoCampus]
    }
    class HorarioPolo {
        polo: Polo!
        dia_semana: Integer!
        horario_funcionamento: HorarioFuncionamentoPolo!
    }
    class HorarioTutorPolo {
        tutor: TutorPolo!
        dia_semana: Integer!
        horario_funcionamento: HorarioFuncionamentoPolo!
    }
    class CoordenadorPolo {
        polo: Polo!
        vinculo: Vinculo!
        titular: Boolean!
    }
    class HorarioCoordenadorPolo {
        coordenador: CoordenadorPolo!
        dia_semana: Integer!
        horario_funcionamento: HorarioFuncionamentoPolo!
    }

    Cidade "1" <-- "n" Polo
    Diretoria "1" <-- "n" Polo
    UnidadeOrganizacional "1" <-- "n" Polo
    Polo "1" --> "n" AtividadePolo
    AtividadePolo "n" <-- "1" Sala
    AtividadePolo "n" <-- "1" IfrnId
    Polo "1" --> "n" HorarioFuncionamentoPolo
    HorarioFuncionamentoPolo "n" <-- "1" Turno
    Polo "1" --> "n" TutorPolo
    TutorPolo "n" <-- "1" IfrnId
    Polo "1" --> "n" HorarioPolo
    HorarioPolo "n" <-- "1" HorarioFuncionamentoPolo
    Polo "1" --> "n" CoordenadorPolo
    CoordenadorPolo "n" <-- "1" IfrnId
    HorarioCoordenadorPolo "1" --> "n" HorarioCoordenadorPolo
    HorarioCoordenadorPolo "n" <-- "1" HorarioFuncionamentoPolo
```

> **HorarioPolo**, **HorarioCoordenadorPolo** e **HorarioTutorPolo**
> 1. dia_semana=`[[1, 'Segunda'], [2, 'Terça'], [3, 'Quarta'], [4, 'Quinta'], [5, 'Sexta'], [6, 'Sábado'], [7, 'Domingo']]`

> **HorarioFuncionamentoPolo**
> 1. numero=`[[1, '1'], [2, '2'], [3, '3'], [4, '4'], [5, '5'], [6, '6']]`
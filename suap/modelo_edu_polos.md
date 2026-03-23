# SUAP Edu

## Polos - Digrama

```mermaid
classDiagram
    class CursoCampus {
        _: VerDiagramaCursos
    }
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
    class TutorPolo {
        polo: Polo!
        vinculo: Vinculo!
        cursos: set[CursoCampus]
    }
    class CoordenadorPolo {
        polo: Polo!
        vinculo: Vinculo!
        titular: Boolean!
    }

    Cidade "1" <-- "n" Polo
    Diretoria "1" <-- "n" Polo
    UnidadeOrganizacional "1" <-- "n" Polo

    Polo "1" --> "n" TutorPolo
    Polo "1" --> "n" CoordenadorPolo
    Polo "1" --> "n" HorarioFuncionamentoPolo
    Polo "1" --> "n" HorarioPolo

    TutorPolo "n" -- "n" CursoCampus
    CoordenadorPolo "n" <-- "1" IfrnId
    TutorPolo "n" <-- "1" IfrnId
```


## Horários dos polos - Digrama

```mermaid
classDiagram
    class IfrnId {
        _: VerDiagramaIfrnId
    }
    class Polo {
        _: VerDiagrama acima
    }
    class TutorPolo {
        polo: Polo!
        vinculo: Vinculo!
        cursos: set[CursoCampus]
    }
    class CoordenadorPolo {
        polo: Polo!
        vinculo: Vinculo!
        titular: Boolean!
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

    Polo "1" --> "n" TutorPolo
    Polo "1" --> "n" CoordenadorPolo
    Polo "1" --> "n" HorarioFuncionamentoPolo
    Polo "1" --> "n" HorarioPolo

    TutorPolo "n" -- "n" CursoCampus
    CoordenadorPolo "n" <-- "1" IfrnId
    TutorPolo "n" <-- "1" IfrnId
  
    HorarioFuncionamentoPolo "1" <-- "n" HorarioPolo
    HorarioFuncionamentoPolo "1" <-- "n" HorarioTutorPolo
    HorarioFuncionamentoPolo "1" <-- "n" HorarioCoordenadorPolo
    HorarioFuncionamentoPolo "n" <-- "1" Turno
```


> **HorarioPolo**, **HorarioCoordenadorPolo** e **HorarioTutorPolo**
> 1. dia_semana=`[[1, 'Segunda'], [2, 'Terça'], [3, 'Quarta'], [4, 'Quinta'], [5, 'Sexta'], [6, 'Sábado'], [7, 'Domingo']]`

> **HorarioFuncionamentoPolo**
> 1. numero=`[[1, '1'], [2, '2'], [3, '3'], [4, '4'], [5, '5'], [6, '6']]`


## Observações

1. Os models abaixo não foram utilizados pois não pareceram ter relevância para a integração:
   1. `edu.polos.AtividadePolo`

1. Os models abaixo podem ser úteis para dar transparência dos horários do coordenadores e tutores no polos, útil para os alunos:
   1. `edu.polos.HorarioFuncionamentoPolo`
   1. `edu.polos.HorarioPolo`
   1. `edu.polos.HorarioTutorPolo`
   1. `edu.cadastros_gerais.Turno`

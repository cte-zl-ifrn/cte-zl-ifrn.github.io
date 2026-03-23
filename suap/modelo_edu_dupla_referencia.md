# SUAP Edu

Referências ambíguas.


## EixoTecnologico - Digrama

```mermaid
classDiagram
    class EixoTecnologico {
        descricao: String!!
        codigo_inep: String
    }
    class CursoTecnico{
        ...
        eixo_tecnologico: EixoTecnologico!
        ...
    }
    class CursoCampus{
        ...
        eixo: EixoTecnologico
        curso_tecnico: CursoTecnico
        ...
    }

    CursoTecnico "n" --> "1" EixoTecnologico
    CursoCampus "n" --> "1" EixoTecnologico
    CursoCampus "n" --> "1" CursoTecnico
```

Dada uma matrícula em um diário, é possível identificar o `EixoTecnologico` de 2 formas, qual usar?

1. `Matricula -> Diario -> Turma -> CursoCampus -> EixoTecnologico`
2. `Matricula -> Diario -> Turma -> CursoCampus -> CursoTecnico -> EixoTecnologico`

## NivelEnsino - Digrama

```mermaid
classDiagram
    class NivelEnsino {
        descricao: String!!
    }
    class Modalidade{
        descricao: String!!
        nivel_ensino: NivelEnsino
    }
    class Componente {
        nivel_ensino: NivelEnsino!
    }
    class ComponenteCurricular {
        componente: Componente!
    }
    class Matriz {
        _: VerDiagramaMatriz
        nivel_ensino: NivelEnsino
        componentes: set[ComponenteCurricular]
    }
    class Aluno {
        nivel_ensino_anterior: NivelEnsino
    }
    class CursoCampus{
        modalidade: Modalidade
    }

    Componente "n" --> "1" NivelEnsino

    Matriz "n" --> "1" NivelEnsino

    Aluno "n" --> "1" NivelEnsino

    ComponenteCurricular "n" --> "1" Componente
    ComponenteCurricular "n" --> "n" Matriz

    MatrizCurso "n" --> "1" CursoCampus
    MatrizCurso "n" --> "1" Matriz

    CursoCampus "n" --> "1" Modalidade
    
    Modalidade "n" --> "1" NivelEnsino
```


Dada uma matrícula em um diário, é possível identificar o `NivelEnsino` de 4 formas, qual usar?

1. `Matricula -> Diario -> Turma -> CursoCampus -> Modalidade -> NivelEnsino`
2. `Matricula -> Diario -> Turma -> CursoCampus -> MatrizCurso -> Matriz -> NivelEnsino`
3. `Matricula -> Diario -> Turma -> CursoCampus -> MatrizCurso -> Matriz -> ComponenteCurricular -> Componente -> NivelEnsino`
4. `Matricula -> Aluno -> NivelEnsino`


## EixoTecnologico - Digrama

```mermaid
classDiagram
    class Turno {
        descricao: String!!
        codigo_enade: String
    }
    class Aluno {
        turno: Turno
        codigo_inep: String
    }
    class Diario {
        turno: Turno
    }
    class Turma {
        turno: Turno
    }
    class TurmaMinicurso {
        turno: Turno
    }
    Turno "1" --> "n" Aluno
    Turno "1" --> "n" Diario
    Turno "1" --> "n" Turma
    Turno "1" --> "n" TurmaMinicurso
```

Dada uma matrícula em um diário, é possível identificar o `Turno` de 4 formas, qual usar?

1. `Aluno -> Turno`
2. `Aluno -> Matricula -> TurmaMiniCurso -> Turno`
3. `Aluno -> Matricula -> Diario -> Turno`
4. `Aluno -> Matricula -> Diario -> Turma -> Turno`


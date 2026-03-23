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

    CursoCampus "n" --> "1" Modalidade
    
    Modalidade "n" --> "1" NivelEnsino
    Componente "n" --> "1" NivelEnsino
    Matriz "n" --> "1" NivelEnsino
    Aluno "n" --> "1" NivelEnsino

    ComponenteCurricular "n" --> "1" Componente
    ComponenteCurricular "n" --> "n" Matriz


    Componente "n" --> "1" NivelEnsino
    Componente "n" --> "1" GrupoAtuacao

    ComponenteCurricular "n" --> "1" Matriz
    ComponenteCurricular "n" --> "1" Componente

    MatrizCurso "n" --> "1" CursoCampus
    MatrizCurso "n" --> "1" Matriz
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

```markdown
## ========= Medidas no arquivo =========
## 01 - Próximo Intervalo
## 02 - Próximo Valor
## 03 - Diferença (R$)
## 04 - Diferença (%)
## 05 - Tipo Período
## ======================================
```

## -------------------------------01 - Próximo Intervalo-------------------------------

```dax
01 - Próximo Intervalo = 
VAR __TipoPeriodo =
    MIN ( 'Tipo Período'[Tipo Período] )

VAR __InicioAtual =
    SWITCH (
        __TipoPeriodo,
        "Ano",       MIN ( dCalendario[Ano] ),
        "Trimestre", MIN ( dCalendario[Ordem Ano e Trimestre] ),
        "Mês",       MIN ( dCalendario[Ordem Ano e Mês] ),
        "Semana",    MIN ( dCalendario[Ordem Ano e Semana] ),
        BLANK ()
    )

VAR __ProximoIntervalo =
    SWITCH (
        __TipoPeriodo,

        "Ano",
            CALCULATE (
                MIN ( dCalendario[Ano] ),
                FILTER (
                    ALLSELECTED ( dCalendario ),
                    dCalendario[Ano] > __InicioAtual
                )
            ),

        "Trimestre",
            CALCULATE (
                MIN ( dCalendario[Ano e Trimestre] ),
                FILTER (
                    ALLSELECTED ( dCalendario ),
                    dCalendario[Ordem Ano e Trimestre] > __InicioAtual
                )
            ),

        "Mês",
            CALCULATE (
                MIN ( dCalendario[Ano e Mês] ),
                FILTER (
                    ALLSELECTED ( dCalendario ),
                    dCalendario[Ordem Ano e Mês] > __InicioAtual
                )
            ),

        "Semana",
            CALCULATE (
                MIN ( dCalendario[Ano e Semana] ),
                FILTER (
                    ALLSELECTED ( dCalendario ),
                    dCalendario[Ordem Ano e Semana] > __InicioAtual
                )
            ),

        BLANK ()
    )

RETURN
    __ProximoIntervalo
```

## -------------------------------02 - Próximo Valor-------------------------------

```dax
02 - Próximo Valor = 
VAR __ProximoIntervalo = [01 - Próximo Intervalo]
VAR __TipoPeriodo = MIN ( 'Tipo Período'[Tipo Período] )
RETURN
SWITCH(
    __TipoPeriodo,
    "Ano",
        CALCULATE(
            [Valor a ser comparado],
            FILTER(
                ALL( dCalendario ),
                dCalendario[Ano] = __ProximoIntervalo
            )
        ),
    "Trimestre",
        CALCULATE(
            [Valor a ser comparado],
            FILTER(
                ALL( dCalendario ),
                dCalendario[Ano e Trimestre] = __ProximoIntervalo
            )
        ),
    "Mês",
        CALCULATE(
            [Valor a ser comparado],
            FILTER(
                ALL( dCalendario ),
                dCalendario[Ano e Mês] = __ProximoIntervalo
            )
        ),
    "Semana",
        CALCULATE(
            [Valor a ser comparado],
            FILTER(
                ALL( dCalendario ),
                dCalendario[Ano e Semana] = __ProximoIntervalo
            )
        )
)
```

## -------------------------------03 - Diferença (R$)-------------------------------

```dax
03 - Diferença (R$) = 
IF( 
    [02 - Próximo Valor] <> BLANK(),
    [02 - Próximo Valor] - [Valor a ser comparado],
    BLANK()
)
```

## -------------------------------04 - Diferença (%)-------------------------------

```dax
04 - Diferença (%) = 
IF( 
    [02 - Próximo Valor] <> BLANK(),

    DIVIDE(
        [02 - Próximo Valor],
        [Valor a ser comparado],
        0
    ) - 1,

    BLANK()
)
```

## -------------------------------05 - Tipo Período-------------------------------

```dax
Tipo Período = {
    ("Ano", NAMEOF('dCalendario'[Ano]), 0),
    ("Trimestre", NAMEOF('dCalendario'[Ano e Trimestre]), 1),
    ("Mês", NAMEOF('dCalendario'[Ano e Mês]), 2),
    ("Semana", NAMEOF(dCalendario[Ano e Semana]), 3)
}
```
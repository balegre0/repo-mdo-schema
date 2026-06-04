graph TD
    Start([Inicio Algoritmo HappyDent]) --> D1[Definir dia, servicio, seguro, validar Como Caracter]
    D1 --> D2[Definir costo Como Entero]
    D2 --> D3[Definir valido como Logico]

    D3 --> A1[valido <- Verdadero]
    A1 --> A2[costo <- 0]

    A2 --> E1[/"Escribir 'ingrese el dia de la cita (Lunes / Martes): '"/]
    E1 --> L1[/Leer dia/]

    L1 --> Si1{¿Minusculas dia <> 'lunes' Y Minusculas dia <> 'martes'?}

    Si1 -- Verdadero --> E2[/Escribir 'Perdon, el consultorio solo atiene los lunes y martes'/]
    E2 --> A3[valido <- Falso]

    Si1 -- Falso --> E3[/"Escribir 'Servicios disponibles:' <br> Escribir '1. Odontologia general' <br> Escribir '2. Ortodoncia' <br> Escribir 'Selecciona el servicio (1 o 2): '"/]
    E3 --> L2[/Leer servicio/]

    L2 --> Si2{¿servicio <> '1' Y servicio <> '2'?}

    Si2 -- Verdadero --> E4[/Escribir 'Opcion de servicio no valida'/]
    E4 --> A4[valido <- Falso]

    Si2 -- Falso --> E5[/"Escribir 'Tienes seguro medico? (S/N): '"/]
    E5 --> L3[/Leer seguro/]
    L3 --> Call[[validar <- ValidarSeguro seguro]]

    Call --> Si3{¿validar = 'error'?}

    Si3 -- Verdadero --> E6[/Escribir 'Opcion de seguro no valida'/]
    E6 --> A5[valido <- Falso]

    Si3 -- Falso --> Si4{¿servicio = '1'?}

    Si4 -- Verdadero --> Si5{¿validar = 's'?}
    Si5 -- Verdadero --> C1[costo <- 1500]
    Si5 -- Falso --> C2[costo <- 1300]

    Si4 -- Falso --> Si6{¿servicio = '2'?}
    Si6 -- Verdadero --> Si7{¿validar = 's'?}
    Si7 -- Verdadero --> C3[costo <- 1700]
    Si7 -- Falso --> C4[costo <- 1500]
    Si6 -- Falso --> Empty[ ]

    C1 --> Join1[ ]
    C2 --> Join1
    C3 --> Join2[ ]
    C4 --> Join2
    Empty --> Join2

    Join1 --> Join3[ ]
    Join2 --> Join3
    A5 --> Join3
    ErrSeg --> Join3

    A4 --> Join4[ ]
    Join3 --> Join4

    A3 --> Join5[ ]
    Join4 --> Join5

    Join5 --> SiFinal{¿valido = Verdadero?}
    SiFinal -- Verdadero --> E7[/Escribir 'Cita procesada para el dia: ', dia <br> Escribir 'Costo de la atencion: RD$', costo/]
    SiFinal -- Falso --> End([Fin Algoritmo])
    E7 --> End

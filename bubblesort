.MODEL SMALL

.STACK 100h

.DATA
    vector DB 10 dup(?)         ; Vectorul care va fi sortat
    marime_vector DB ?          ; Dimensiunea vectorului, introdusa de utilizator
    prompt_size DB 'Introduceti dimensiunea vectorului (3-9): $'
    prompt_invalid_size DB ' Dimensiunea trebuie sa fie intre 3 si 9! Inchide si redeschide algoritmul pentru a incerca din nou.$'
    prompt_number DB ' Introduceti un numar: $'
    prompt_invalid_input DB ' Numarul introdus este invalid! Inchide si redeschide algoritmul pentru a incerca din nou.$'
    mesaj_sortat DB ' Vectorul sortat este: $'

.CODE
MAIN PROC
    MOV AX, @DATA               ; Initializare clasica a segmentului de date
    MOV DS, AX

    CALL citire_vector          ; Apelare functie

    LEA SI, vector              ; Pointer catre inceputul vectorului
    MOV CL, marime_vector       ; Dimensiunea vectorului
    DEC CL                      ; CL = array_size - 1 (numar de pasi)

outer_loop:
    PUSH CX                     ; Salveaza CX pentru bucla exterioara
    LEA SI, vector              ; Reincarca pointerul catre inceputul vectorului
    MOV CL, marime_vector       ; Reincarca dimensiunea vectorului
    DEC CL                      ; CL = array_size - 1

swap_elemente:
    MOV AL, [SI]                ; AL = elementul curent
    MOV BL, [SI+1]              ; BL = urmatorul element

    CMP AL, BL                  ; Compara elementele
    JBE zero_modificari         ; Daca al <= bl, nu se schimba

    ; Schimba elementele folosind un registru intermediar
    MOV DL, [SI+1]              ; DL = urmatorul element
    MOV [SI+1], AL              ; Urmatorul element primeste valoarea curentului
    MOV [SI], DL                ; Elementul curent primeste valoarea urmatorului

zero_modificari:
    INC SI                      ; Treci la urmatorul element
    LOOP swap_elemente          ; Repeta pana la sfarsitul vectorului

    POP CX                      ; Restaureaza CX pentru bucla exterioara
    LOOP outer_loop             ; Repeta bucla exterioara

    ; Finalizare sortare
    MOV AH, 9                   ; Afiseaza mesajul "Vectorul sortat este"
    LEA DX, mesaj_sortat
    INT 21h

    CALL afisare_vector_sortat  ; Afiseaza vectorul sortat

    MOV AH, 4Ch                 ; Termina programul
    INT 21h
MAIN ENDP

; Subrutina pentru citirea vectorului de la utilizator
citire_vector:
    MOV AH, 9                   ; Afiseaza mesajul pentru introducerea dimensiunii
    LEA DX, prompt_size
    INT 21h

    CALL citire_cifra           ; Citeste dimensiunea
    CMP AL, 3                   ; Verifica daca dimensiunea este intre 3...
    JB invalid_size
    CMP AL, 10                  ; ... si 10
    JAE invalid_size

    MOV marime_vector, AL       ; Salveaza dimensiunea in marime_vector
    LEA SI, vector              ; Pointer la inceputul vectorului
    MOV CL, marime_vector       ; Pregateste numarul de elemente de citit

read_loop:
    MOV AH, 9                   ; Afiseaza mesajul pentru introducerea unui numar
    LEA DX, prompt_number
    INT 21h

    CALL citire_cifra           ; Citeste numarul
    CMP AL, 0                   ; Verifica daca inputul este valid (>= 0)
    JL invalid_input
    CMP AL, 10                  ; Verifica daca inputul este valid (< 10)
    JGE invalid_input

    MOV [SI], AL                ; Salveaza numarul in vector
    INC SI                      ; Treci la urmatoarea pozitie

    MOV AH, 2                   ; Afiseaza un spatiu dupa fiecare numar
    MOV DL, ' '                 ; Seteaza caracterul de spatiu
    INT 21h

    LOOP read_loop              ; Continua pana se citesc toate elementele
    RET

invalid_size:
    MOV AH, 9                   ; Afiseaza mesajul de eroare
    LEA DX, prompt_invalid_size
    INT 21h
    MOV AH, 4Ch                 ; Termina programul
    INT 21h

invalid_input:
    MOV AH, 9                   ; Afiseaza mesajul de input invalid
    LEA DX, prompt_invalid_input
    INT 21h
    MOV AH, 4Ch                 ; Termina programul
    INT 21h

; Subrutina pentru citirea unei cifre
citire_cifra:
    MOV AH, 1                   ; Functie DOS pentru citirea unei taste
    INT 21h
    CMP AL, '0'                 ; Verifica daca este in intervalul valid
    JL invalid_digit
    CMP AL, '9'
    JG invalid_digit
    SUB AL, 30h                 ; Transforma codul ASCII in valoare numerica
    RET

invalid_digit:
    MOV AL, -1                  ; Seteaza un cod invalid
    RET

; Subrutina pentru afisarea vectorului sortat
afisare_vector_sortat:
    LEA SI, vector              ; Pointer la inceputul vectorului
    MOV CL, marime_vector       ; Dimensiunea vectorului

loop_afisare:
    MOV AL, [SI]                ; AL = elementul curent
    CALL afisare_cifra          ; Afiseaza cifra

    MOV AH, 2                   ; Functie DOS pentru afisare caracter
    MOV DL, ' '                 ; Afiseaza un spatiu intre numere
    INT 21h

    INC SI                      ; Treci la urmatorul element
    LOOP loop_afisare           ; Continua pana cand toate elementele sunt afisate
    RET

; Subrutina pentru afisarea unei cifre
afisare_cifra:
    ADD AL, 30h                 ; Transforma cifra din valoare numerica in cod ASCII
    MOV AH, 2                   ; Functie DOS pentru afisare caracter
    MOV DL, AL                  ; Pune caracterul in DL pentru afisare
    INT 21h
    RET

END MAIN

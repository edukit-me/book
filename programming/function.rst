Funcții
=======

Funcțiile sunt grupuri de întrucțiuni (bucăți de cod)
care primesc niște variabile sub formă de parametri și returnează un rezultat (niște date).
Acestea vă ajută să nu repetați codul, să îl scrieți mai compact și mai organizat.

De exemplu, pentru a face led-ul de pe placa Arduino
să clipească la interval de o secundă de 2 apoi de 3 ori,
fără funcții programul este următorul:

.. code-block:: cpp

    void setup() {
        pinMode(13, OUTPUT);

        digitalWrite(13, HIGH);
        // ține led-ul aprins 5 secunde pentru a înțelege
        // cînd o să înceapă să clipească
        delay(5000);
        digitalWrite(13, LOW);
        delay(1000);

        digitalWrite(13, HIGH);
        delay(200);
        digitalWrite(13, LOW);
        delay(200);
        digitalWrite(13, HIGH);
        delay(200);
        digitalWrite(13, LOW);

        delay(1000);

        digitalWrite(13, HIGH);
        delay(200);
        digitalWrite(13, LOW);
        delay(200);
        digitalWrite(13, HIGH);
        delay(200);
        digitalWrite(13, LOW);
        delay(200);
        digitalWrite(13, HIGH);
        delay(200);
        digitalWrite(13, LOW);
    }

    void loop() {}

Programul se primește prea mare,
imaginați-vă cît de mare o să fie în caz că vrem să facem led-ul să clipească de 10 ori.

Structura unei funții este:

.. code-block:: text

    tipul_rezultatului numele_funcțeie(tipul_parametrului numele_parametrului) {
        instrucțiuni...

        return rezultatul;
    }

Mai jos este același program dar îmbunătățit cu ajutorul intrucțiunii ``for`` și a unei funcții.

.. code-block:: cpp

    void clipire(int numarul_de_clipiri) {
        for (
            int clipiri_efectuate = 0;
            clipiri_efectuate < numarul_de_clipiri;
            ++clipiri_efectuate
        ) {
            digitalWrite(13, HIGH);
            delay(200);
            digitalWrite(13, LOW);
            delay(200);
        }

        delay(1000);
    }

    void setup() {
        pinMode(13, OUTPUT);

        digitalWrite(13, HIGH);
        // ține led-ul aprins 5 secunde pentru a înțelege
        // cînd o să înceapă să clipească
        delay(5000);
        digitalWrite(13, LOW);
        delay(1000);

        clipire(2);
        clipire(3);
    }

    void loop() {}

.. note::

    Cele 3 componente ale instrucțiunii ``for`` au fost scrise din rînd nou
    pentru ca programul să fie mai citibil.
    În C++ nu contează dacă e din rînd nou sau nu, puteți scrie chiar tot programul într-un rînd,
    dar el va fi greu de înțeles.

.. note::

    La funcțiile care nu returnează nici un rezultat se indică ``void``.

Funcția ``clipire`` se traduce ca: Crează variabila ``clipiri_efectuate`` de tip ``int`` *(număr întreg)*
și setează-i valoarea ``0``. Atîta timp cît numărul de clipiri efectuate este mai mic decît
numărul de clipiri care trebuiesc făcute, aprinde led-ul, așteată ``200`` milisecunde,
stinge led-ul, așteaptă ``200`` milisecunde, și mărește numărul de clipiri efectuate cu ``1``.
Apoi așteaptă o secundă.

Acum puteți ușor schimba programul să clipească de cîte ori doriți, modificînd foarte puțin cod.

Funcția ``clipire`` poate fi schimbată să accepte un al doilea parametru: **durata clipirii**
(la moment aceasta este ``200`` milisecunde). Înlocuiți funcția cu:

.. code-block:: cpp

    void clipire(int numarul_de_clipiri, int durata_clipirii = 200) {
        for (
            int clipiri_efectuate = 0;
            clipiri_efectuate < numarul_de_clipiri;
            ++clipiri_efectuate
        ) {
            digitalWrite(13, HIGH);
            delay(durata_clipirii);
            digitalWrite(13, LOW);
            delay(durata_clipirii);
        }

        delay(1000);
    }

.. note::

    ``= 100`` de la al doilea parametru înseamnă ca acesta este opțional
    și dacă nu va fi indicat, atunci va primi valoarea implicită ``100``.

Modificați programul și apelați funcția cu diferiți parametri:

.. code-block:: cpp

    clipire(2);
    clipire(3, 500);
    clipire(7, 30);

Funcția loop()
--------------

Spre deosebire de funcția ``setup()`` care se execută o singură data,
funcția ``loop()`` se repeată la infinit.
În exemplele precedente ați scris programele în funcția ``setup()``
pentru ca ele să se execute o singură dată și să fie mai ușor de înțeles cum acestea funcționează.
De obicei toată logica programelor pe Ardiuno se scrie în funcția ``loop()``
pentru că Arduino trebuie permanent să primească informație de la senzori și să o prelucreze,
de exemplu: o seră trebuie închisă noaptea și deschisă dimineața, sau
o mașină cu autopilot trebuie să se ferească de obstacole.

(todo: exemplu cu senzor de lumina si clipire)
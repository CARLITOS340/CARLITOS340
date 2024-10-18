int entradas[] = {2, 3, 4, 5, 6, 7, 8}; // Pines conectados a los segmentos a, b, c, d, e, f, g del display
int boton = 9; // Pin conectado al botón
int boton2 = 10; // Pin conectado al botón
int boton3 = 11; // Pin conectado al botón
int counter = 0;
int led = 12;

// Valores hexadecimales para mostrar números del 0 al 9 en un display de 7 segmentos (cátodo común)
byte numbers[] = {
  0x3F, // 0
  0x06, // 1
  0x5B, // 2
  0x4F, // 3
  0x66, // 4
  0x6D, // 5
  0x7C, // 6
  0x07, // 7
  0x7F, // 8
  0x67  // 9
};

void setup() {
  for (int i = 0; i < 7; i++) {
    pinMode(entradas[i], OUTPUT); // Configura todos los pines de los segmentos como salida
  }

  pinMode(led, OUTPUT);
  pinMode(led, LOW);
  pinMode(boton, INPUT_PULLUP); // Configura el pin del botón como entrada con resistencia pull-up
  displayNumber(counter); // Muestra el número inicial
}

void loop() {
  //int estadoBoton = digitalRead(boton); // Lee el estado del botón

  // Detecta si se presionó y soltó el botón
  if (digitalRead(boton) == LOW) {
    counter++; // Incrementa el contador
    if (counter > 3) {
      counter = 3; // Reinicia el contador si supera 9
    }
    displayNumber(counter); // Muestra el número en el display
    delay(200); // Pequeña espera para evitar rebotes
  }

  if (digitalRead(boton2) == LOW) {
    counter--; // Incrementa el contador
    if (counter < 0) {
      counter = 0; // Reinicia el contador si supera 9
    }
    displayNumber(counter); // Muestra el número en el display
    delay(200); // Pequeña espera para evitar rebotes
  }

  if(digitalRead(boton3) == LOW){
    if(counter == 1){
        pinMode(led, HIGH);
        delay(1000);
        pinMode(led, LOW);
      }
    }

  if(digitalRead(boton3) == LOW){
    if(counter == 2){
        pinMode(led, HIGH);
        delay(100);
        pinMode(led, LOW);
      }
    }

    if(digitalRead(boton3) == LOW){
    if(counter == 3){
        pinMode(led, HIGH);
        delay(1000);
        pinMode(led, LOW);
        delay(1000);
      }
    }
}

void displayNumber(int num) {
  byte segments = numbers[num]; // Obtén el patrón de segmentos para el número
  for (int i = 0; i < 7; i++) {
    digitalWrite(entradas[i], bitRead(segments, i)); // Actualiza cada segmento individualmente
  }
}

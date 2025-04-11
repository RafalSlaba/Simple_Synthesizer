void setup() {
    // inicjalizacja uartu
    Serial.begin(9600);

    // ustawianie pinów od 27 do 51 jako wejścia z rezystorami podciągającymi do zasilania
    for (int pin = 27; pin <= 51; pin += 2) {
        pinMode(pin, INPUT_PULLUP); 
    }
}

void loop() {
    int activePin = -1;

    // sprawdzanie stanu pinów
    for (int pin = 27; pin <= 51; pin += 2) {
        int bitValue = digitalRead(pin);

        // Adjust for active LOW (since pull-up resistors are used)
        if (!bitValue) { // czy przycisk wciśnięty
            activePin = ((51 - pin) / 2) + 1; // dana do wysłania w zależności od przycisku
        }
    }

    if (activePin != -1) {
        Serial.println(activePin); // wysyłanie danych
    }
    delay(100);
}

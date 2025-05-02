#include <stdio.h>
#include <stdlib.h>
//Velázquez Herrera María Thais Itzel 3CV4
#define MAX 1000  // Tamaño máximo de la secuencia de Fibonacci
// Función para saber si un número es primo
int esPrimo(int n) {
    if (n < 2) return 0;
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) return 0;
    }
    return 1;
}
// Función para generar la secuencia de Fibonacci filtrada
int generarFibonacciFiltrado(int fib[]) {
    int a = 0, b = 1, c, pos = 1, size = 0;
    fib[size++] = a;  // Posición 1 (0)
    fib[size++] = b;  // Posición 2 (1)
    while (1) {
        c = a + b;
        pos++;
        // Detener si el número es muy grande
        if (c > 1000000) break;
        // Guardar solo si la posición NO es prima
        if (!esPrimo(pos)) {
            fib[size++] = c;
        }
        a = b;
        b = c;
    }
    return size; // Retornar cuántos números se generaron
}

// Función recursiva para encontrar los términos de suma mínima
void encontrarSuma(int fib[], int size, int k) {
    if (k == 0) return;
    // Buscar el número más grande <= k
    int i;
    for (i = size - 1; i >= 0; --i) {
        if (fib[i] <= k) {
            printf("%d ", fib[i]);
            encontrarSuma(fib, i - 1, k - fib[i]);
            break;
        }
    }
}

// Función para calcular el valor de K
int calcularK(int dia, int mes, int anio) {
    return (dia + 100) * (mes + 10) + (anio % 100);
}

// Programa principal
int main() {
    int dia, mes, anio;
    int K;
    int fib[MAX];
    int size;
    // Entrada del usuario
    printf("Ingrese su dia de nacimiento: ");
    scanf("%d", &dia);
    printf("Ingrese su mes de nacimiento: ");
    scanf("%d", &mes);
    printf("Ingrese su anio de nacimiento: ");
    scanf("%d", &anio);
    // Calcular K
    K = calcularK(dia, mes, anio);
    printf("\nValor de K: %d\n", K);
    // Generar secuencia de Fibonacci filtrada
    size = generarFibonacciFiltrado(fib);
    printf("Terminos seleccionados:\n");
    encontrarSuma(fib, size, K);
    printf("\n");
    return 0;
}


# PARCIAL-CORTE-2-
#include <iostream>
using namespace std;

int main() {
    const int filas = 6;
    const int columnas = 7;
    char tablero[filas][columnas];

    for (int i = 0; i < filas; i++) {
        for (int j = 0; j < columnas; j++) {
            tablero[i][j] = '.';
        }
    }

    cout << "tablero:" << endl;
    for (int i = 0; i < filas; i++) {
        for (int j = 0; j < columnas; j++) {
            cout << tablero[i][j] << " ";
        }
        cout << endl;
    }

    int turno = 1;
    bool victoria = false;
    int movimientos = 0;
    int maxMovimientos = filas * columnas;

    while (!victoria && movimientos < maxMovimientos) {
        char ficha;
        if (turno == 1) {
            ficha = 'X';
        } else {
            ficha = 'O';
        }

        cout << endl << "Turno del jugador " << turno << " (" << ficha << ")" << endl;
        cout << "Elige una columna (0 a 6): ";
        int columna;
        cin >> columna;

        while (columna < 0 || columna >= columnas) {
            cout << "Esa columna no existe, intenta de nuevo: ";
            cin >> columna;
        }

        bool colocada = false;
        for (int i = filas - 1; i >= 0; i--) {
            if (tablero[i][columna] == '.') {
                tablero[i][columna] = ficha;
                colocada = true;
                break;
            }
        }

        if (!colocada) {
            cout << "Esa columna ya esta llena, elige otra." << endl;
            continue;
        }

        movimientos++;

        cout << endl << "Tablero actualizado:" << endl;
        for (int i = 0; i < filas; i++) {
            for (int j = 0; j < columnas; j++) {
                cout << tablero[i][j] << " ";
            }
            cout << endl;
        }

        for (int i = 0; i < filas; i++) {
            for (int j = 0; j < columnas - 3; j++) {
                if (tablero[i][j] == ficha && tablero[i][j + 1] == ficha &&
                    tablero[i][j + 2] == ficha && tablero[i][j + 3] == ficha) {
                    victoria = true;
                }
            }
        }

        for (int i = 0; i < filas - 3; i++) {
            for (int j = 0; j < columnas; j++) {
                if (tablero[i][j] == ficha && tablero[i + 1][j] == ficha &&
                    tablero[i + 2][j] == ficha && tablero[i + 3][j] == ficha) {
                    victoria = true;
                }
            }
        }

        for (int i = 0; i < filas - 3; i++) {
            for (int j = 0; j < columnas - 3; j++) {
                if (tablero[i][j] == ficha && tablero[i + 1][j + 1] == ficha &&
                    tablero[i + 2][j + 2] == ficha && tablero[i + 3][j + 3] == ficha) {
                    victoria = true;
                }
            }
        }

        for (int i = 0; i < filas - 3; i++) {
            for (int j = 3; j < columnas; j++) {
                if (tablero[i][j] == ficha && tablero[i + 1][j - 1] == ficha &&
                    tablero[i + 2][j - 2] == ficha && tablero[i + 3][j - 3] == ficha) {
                    victoria = true;
                }
            }
        }

        if (victoria) {
            cout << endl << "El jugador " << turno << " (" << ficha << ") ha ganado!" << endl;
            break;
        }

        if (turno == 1) {
            turno = 2;
        } else {
            turno = 1;
        }
    }

    if (!victoria) {
        cout << endl << "El juego termino en empate." << endl;
    }

    char otraVez;
    cout << "¿Quieres jugar de nuevo? (s/n): ";
    cin >> otraVez;

    if (otraVez == 's' || otraVez == 'S') {
        main();
    } else {
        cout << "Gracias por jugar Conecta 4 :)" << endl;
    }

    return 0;
}

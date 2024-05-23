#include <stdio.h>

#include <string.h>

#include <stdlib.h>



struct empleados {

    long int cc;

    char nombre[20];

    char cargo[20];

    char estado[20];

    long int salario;

};



void leer(int *tam);

void mostrar(int tam);

void menu();



struct empleados VectA[10];

int tam; 



void leer(int *tam) {

    int i;



    printf("Cuantos empleados desea almacenar?: ");

    scanf("%d", tam);

    printf("\n");

    for (i = 0; i < *tam; i++) {

        printf("\nIngrese la cedula del trabajador en VectA[%d]: ", i);

        scanf("%li", &VectA[i].cc);

        printf("Ingrese el nombre del trabajador en VectA[%d]: ", i);

        scanf("%s", VectA[i].nombre);

        printf("Ingrese el cargo del trabajador en VectA[%d]: ", i);

        scanf("%s", VectA[i].cargo);

        printf("Ingrese el estado civil del trabajador en VectA[%d]: ", i);

        scanf("%s", VectA[i].estado);

        printf("Ingrese el salario del trabajador en VectA[%d]: ", i);

        scanf("%li", &VectA[i].salario);

        printf("\n");

    }

}



void mostrar(int tam) {

    int i;



    printf("DATOS DE LOS TRABAJADORES \n\n");

    for (i = 0; i < tam; i++) {

        printf("---------------------------------------\n");

        printf("Cedula del trabajador en VectA[%d]: %li\n", i, VectA[i].cc);

        printf("Nombre del trabajador en VectA[%d]: %s\n", i, VectA[i].nombre);

        printf("Cargo del trabajador en VectA[%d]: %s\n", i, VectA[i].cargo);

        printf("Estado civil del trabajador en VectA[%d]: %s\n", i, VectA[i].estado);

        printf("Salario del trabajador en VectA[%d]: %li\n", i, VectA[i].salario);

        printf("---------------------------------------\n");

    }

    system("pause");

}





void quick(struct empleados array[], int min, int max) {

    int i = min;

    int j = max;

    struct empleados temp;

    long int pivot = array[(min + max) / 2].salario;



    do {

        while (array[i].salario < pivot && i < max)

            i++;

        while (array[j].salario > pivot && j > min)

            j--;

        if (i <= j) {

            temp = array[i];

            array[i] = array[j];

            array[j] = temp;

            i++;

            j--;

        }

    } while (i <= j);



    if (min < j)

        quick(array, min, j);

    if (i < max)

        quick(array, i, max);

}



void ordenarEmpleadosPorSalario(int tam) {

    if (tam > 1) {

        quick(VectA, 0, tam - 1);

    }

    printf("Empleados ordenados por salario.\n");

    mostrar(tam);

}



void menu() {

    int opc;



    printf("BIENVENIDO A LA EMPRESA ESTDAT\n\n");

    printf("---------------------------------------\n");

    printf("1. Ingresar los datos de los trabajadores a almacenar\n");

    printf("2. Visualizar los datos de los trabajadores almacenados\n");

    printf("3. Ordenar empleados por salario\n");

    printf("4. Salir\n");

    printf("---------------------------------------\n");

    printf("Digite la opcion deseada: ");

    scanf("%d", &opc);

    switch (opc) {

        case 1: {

            leer(&tam);

            menu();

            break;

        }

        case 2: {

            mostrar(tam);

            menu();

            break;

        }

        case 3: {

            ordenarEmpleadosPorSalario(tam);

            break;

        }

    

        case 4: {

            exit(0);

            break;

        }



        default: {

            printf("Opcion no disponible\n");

            printf("Intente nuevamente\n");

            system("pause");

            menu();

        }

    }

}



int main() {

    menu();

    return 0;


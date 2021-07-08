
// INTEGRANTES: ANTONELLA PERALTA, PORTILLO DAIRA, SANTIAGO ERNST.

#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <string.h> //para poder escribir los nombres

struct registro{ //armamos una estructura para registrar a cada persona.
    int dni;
    char nombre[40]; //para poder escribir
    char apellido[45];
    int nacimiento;
    int edad;
    int telefono;
    char cumple[50];
};

int main (){
  setlocale(LC_ALL,"spanish"); // con esto se puede ver correctamente las letras con tilde y caracteres especiales.
  struct registro registro_datos[5]; // vamos a registrar 5 personas sólo para probar (max 100)
 /* int dni[3];
  char nombre[3];
  char apellidos[3];
  int nacimiento[3];
  int edad[3];
  int telefono[3]; */

 char nuevo_char[5]; // variable por si el usuario edita los datos
int opc=1, num_dni, contador, nuevo;
int i=0, j, buscar, indice_mayor, salir;

while(opc!=0){
    printf("1. Registrar persona.\n2. Ver personas registradas.\n3. Ver personas por año.\n4. Persona más joven.\n5. Editar registro persona.\n6. Buscar persona por DNI.\n0. Salir.\n");
    printf ("\nOpción: ");
    scanf("%i",&opc);
    printf("\n");

    switch(opc){ //depende de la opcion que elija el usuario haremos
        case 1:
            printf("Ingrese número de DNI de la persona: \n");
            scanf("%i",&num_dni);
            contador=0;
            for(j=0; j<i; j++){
                if(num_dni==registro_datos[j].dni){
                    contador++;} // del if
            } //del for

            if(contador==0){ // si elcontador esta en 0 entonces empecemos a registrar a las personas.
                registro_datos[i].dni=num_dni;
                printf("Ingrese nombre de la persona con DNI numero: %i\n",registro_datos[i].dni);
                getchar(); //para leer cadenas de varios caracteres.
                fgets(registro_datos[i].nombre,40,stdin);
           //La funcion fgets se encargara de leer o almacenar una cadena de caracteres introducida mediante el teclado.

                printf("Ingrese apellidos de la persona con DNI número: %i\n",registro_datos[i].dni);
                fgets(registro_datos[i].apellido,45, stdin);

                printf("Ingrese cumpleaños de la persona: \n", registro_datos[i].cumple);
                fgets (registro_datos[i].cumple,50,stdin);

                printf("Ingrese año de nacimiento de la persona con DNI número: %i\n",registro_datos[i].dni);
                scanf("%i",&registro_datos[i].nacimiento);
                //PEDIMOS AÑO PARA MOSTRAR A TODAS LAS PERSONAS NACIDAS EN UN AÑO ESPECIFICO.

                printf("Ingrese la edad de la persona con DNI número: %i\n",registro_datos[i].dni);
                scanf("%i",&registro_datos[i].edad);

                printf ("Ingrese el teléfono de la persona con DNI número: %i\n",registro_datos[i].telefono);
                scanf("%i",&registro_datos[i].telefono);
                i++;
            }else{
                printf("Este número de identificación ya existe, no puede continuar con el registro.\n");
            } // del else.
        break; // fin del case 1.

        case 2: // Mostrará la cantidad de persona en nuestra agenda.
            if(i==0){ // si la cantidad de personas que registraron es igual a 0 entonces:
                printf("Aún no hay personas registradas");
            }else{ //sino mostrarme a quiénes registrar
                printf("Total de personas registradas: %i\n",i);
                for (j = 0; j < i; j++) { // se repetira esta lista con cada dato que registramos.
                    printf("Persona:\t%i\n",(j+1));
                    printf("Nombres:\t%s\n",registro_datos[j].nombre);
                    printf("Apellidos:\t%s\n",registro_datos[j].apellido);
                    printf ("Cumpleaños:\t%s\n",registro_datos[j].cumple);
                    printf("Año de nacimiento:%i\n",registro_datos[j].nacimiento);
                    printf("Edad:\t%i\n\n",registro_datos[j].edad);
                    printf("Telefono:\t%i\n",registro_datos[j].telefono);
                    printf ("--------------------------------");

            } // del for.
            } //del else;
                     break; //fin del case 2.

        case 3: //listado de todas las personas nacidas en un año especifico
            printf("Ingrese año a buscar entre los registros: \n");
            scanf("%i",&buscar);
            contador=0;

            for(j=0; j<i; j++){ //para que busque todas las personas que se registraron
                if(buscar==registro_datos[j].nacimiento){
                    contador++; // que vaya imprimiendo en pantalla a medida que va encontrando
                    printf("Coincidencia: %i\n",contador);
                    printf("Nombres:\t%s\n",registro_datos[j].nombre);
                    printf("Apellidos:\t%s\n",registro_datos[j].apellido);
                    printf("Año de nacimiento:\t%i\n",registro_datos[j].nacimiento);
                    printf("Edad:\t%i\n",registro_datos[j].edad);
                    printf ("-------------------------------------\n");
                } // del if.
            } // del for.

            if (contador==0){
                printf("Sin resultados en la búsqueda."); } //if.
               break; //fin del case 3.

        case 4: // ver quien es la persona mas joven.
            buscar=registro_datos[0].edad;
            indice_mayor=-1;
            for(j=0; j<i; j++){ // un for que recorra todos los datos de las personas registradas y busque
                if(registro_datos[j].edad<=buscar){
                    buscar=registro_datos[j].edad;
                    indice_mayor=j;
                } //del if
            } //del for

            if(indice_mayor!=-1){// mostramos quien es la persona mas joven y sus datos
                printf("Persona más joven.\n");
                printf("DNI: %i\n",registro_datos[indice_mayor].dni);
                printf("Nombres: %s %s",registro_datos[indice_mayor].nombre, registro_datos[indice_mayor].apellido);
                printf("Edad: %i\n",registro_datos[indice_mayor].edad);
            }else{ // si el ciclo for no lo encuentra entonces:
                printf("No hay persona más joven o aún no hay personas registradas.");
            }
        break; //fin del case 4

   /*---------------- separador para entender mejor el case 5, porque es muy largo-----------------------*/

           case 5: //Para poder editar los datos de algun usuario.
                printf("Ingrese DNI de la persona a editar datos: \n");
                scanf("%i",&buscar); // buscaremos por su dni para identificarla y asi cambiar los datos.
                contador=0;
               for(j=0; j<i; j++){ // un ciclo para que vaya recorriendo
                  if(buscar==registro_datos[j].dni){
                    contador++;
                    indice_mayor=j; } //del if.
                   } // del for.

            if(contador==1){
                salir=1;
           while(salir!=0){ //armamos un ciclo para que se repita si es que el usuario quiere modificar mas de una cosa
           printf("1. Número DNI.\n2. Nombre\n3. Apellido\n4. Año de nacimiento.\n5. Edad\n0. Terminar.\n");
           scanf("%i",&salir);

                    switch(salir){ //armamos otro switch para que el usuario decida qué es lo que quiere editar.

                        case 1: // si quiero cambiar su dni
                            printf("Ingrese nuevo número de DNI: \n");
                            scanf("%i",&nuevo);
                            contador=0;
                            for(j=0; j<i; j++){
                                if(nuevo==registro_datos[j].dni){
                                    contador++; } //del if
                            } // del for
                            if(contador==0){
                                registro_datos[indice_mayor].dni=nuevo;
                                printf("Número de DNI cambiado.\n");
                            }else{ // por si el usuario ya agrego a alguien con este dni en vez de cambiarlo y no se dio cuenta
                                printf("%i Este número de DNI ya existe, intente con otro.",nuevo);
                            } // del else
                        break;

          case 2: //cambiar su nombre

                printf("Ingrese nuevo nombre: \n");
                getchar();
                 fgets(nuevo_char, 45, stdin); // donde se guardara el nuevo nombre
                 strcpy(registro_datos[indice_mayor].nombre,nuevo_char);
    //strcpy recibe dos parámetros, primero la string donde se va a copiar el contenido, y segundo la string del cual será copiado su contenido
                 printf("Nombre cambiado.\n");
                 break;

          case 3:
                getchar();
                 printf("Ingrese nuevo apellido: \n");
                 fgets(nuevo_char,45, stdin);
                 strcpy(registro_datos[indice_mayor].apellido,nuevo_char);
                 printf("Apellido cambiado.\n");
                 break;

          case 4:
                 printf("Ingrese nuevo año de nacimiento: \n");
                 scanf("%i",&nuevo);
                 registro_datos[indice_mayor].nacimiento=nuevo;
                 printf("Año de nacimiento cambiado.\n");
                 break;

          case 5:
                printf("Ingrese nueva edad: \n");
                scanf("%i",&nuevo);
                 registro_datos[indice_mayor].edad=nuevo;
                 printf("Edad cambiada.\n");
                 break;


          case 6:
            printf ("Ingrese nuevo teléfono: \n");
            scanf ("i", &nuevo);
            registro_datos[indice_mayor].telefono=nuevo;
            printf ("Teléfono cambiado.\n");
            break;

          case 7:
            getchar();
            printf ("Ingrese nueva fecha de cumpleaños: \n");
             fgets(nuevo_char,50, stdin);
           strcpy(registro_datos[indice_mayor].cumple,nuevo_char);
           printf ("Cumpleaños cambiado.\n");
           break;
            } // del switch
            } // del while
            } // del if donde sirve para editar los datos del usuario.
            break;


       /*--------------------- Fin del separador del case 5 ------------------------------------*/

           case 6:
                printf("Ingrese identificación de la persona a buscar: ");
                scanf("%i",&buscar);
                contador=0;
                for(j=0; j<i; j++){
                    if(buscar==registro_datos[j].dni){
                        printf("Identificación: %i\n",registro_datos[j].dni);
                        printf("Nombre: %s\n",registro_datos[j].nombre);
                        printf("Apellido: %s\n",registro_datos[j].apellido);
                        printf("Año de nacimiento: %i\n",registro_datos[j].nacimiento);
                        printf("Edad: %i\n",registro_datos[j].edad);
                        contador++;
                    } //del if
                } // del for.
                if(contador==0){
                    printf("Sin resultados."); } //del if
            break; // fin del case 6

    } // del primer switch.
    printf("\n");
    system("pause"); // se espera a que el usuario presione alguna tecla para continuar con la ejecución del programa.
    system("cls"); // para limpiar la pantalla del menú.
} // del primer while
  return 0;
}

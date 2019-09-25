# Luis_Ramirez_1358

import xlrd
class Array3D:
    def __init__(self,row,col,deep):
        self.__x=row
        self.__y=col
        self.__z=deep
        self.__cubo=[[[None for x in range(self.__x)] for y in range(self.__y)] for z in range(self.__z)]

    def to_string(self):
        print(self.__cubo)
    def get_num_x(self):
        return self.__x
    def get_num_y(self):
        return self.__y
    def get_num_z(self):
        return self.__z
    def set_item(self,x,y,z,value):
        self.__cubo[z][y][x]=value
    def get_item(self,x,y,z):
        return self.__cubo[z][y][x]
    def clearing(self,value):
        for i in range(self.__z):
            for j in range(self.__y):
                for k in range(self.__x):
                    self.__cubo[i][j][k]=value

def main():        
    print("El siguiente programa permite la organizacaión y consulta de datos mediante un arreglo Array de tres dimensiones")
    data=Array3D(35,14,34)
    for anio in range(1985,2019,1):
        for x in range(35):
            for y in range(14):
                Archivo = xlrd.open_workbook(filename="./Precipitacion/"+str(anio)+"Precip.xls")
                hoja=Archivo.sheet_by_index(0)
                data.set_item(x,y,anio-1985,hoja.cell_value(x,y))
        pass
    Salida=False
    regreso_al_menu_principal=False
    regreso_al_menu=False
    Anio=None
    mes=None
    estado=None
    while Salida !=True:
        anio=None
        anio=int(input("Ingrese un año o cero para salir: "))
        if anio > 1984 and anio <= 2018:
            while regreso_al_menu_principal!=True:
                estado=None
                print("Ingrse el estado o el No. nacional,          Ingrese CERO para regresar al menu principal): ")
                for i in range(data.get_num_x()-2):
                    print(f"{i+1}) {data.get_item(i+2,0,anio-1985)}")
                    pass
                estado=int(input("Opcion: "))
                if estado>=1 and estado<=33:
                    while regreso_al_menu!=True:
                        print("Ingrese el mes.          Ingrese CERO para regresar: ")
                        for i in range(data.get_num_y()-1):
                            print(f"{i+1} {data.get_item(1,i+1,anio-1985)}")
                            pass
                        mes=int(input("Opcion: "))
                        if mes>=1 and mes<=13:
                            print(f"Precipitacion promedio en {anio} en {data.get_item(estado+1,0,0)} el mes de {data.get_item(1,mes,0)} fue: {data.get_item(estado+1,mes,anio-1985)}")
                            print(" - - - - - - - - - - - - - - - - - - -")
                            regreso_al_menu=True
                            regreso_al_menu_principal=True
                            pass
                        elif mes==0:
                            regreso_al_menu=True
                            pass
                        else:
                            print("OPCION INVALIDA")
                            pass
                        pass
                    regreso_al_menu=False
                    pass
                elif estado==0:
                    regreso_al_menu_principal=True
                    pass
                else:
                    print("OPCION INVALIDA")
                    pass
                pass
            regreso_al_menu_principal=False
            pass#fin primer if
        
        elif anio==0:
            print("CONSULTA FINALIZADA")
            Salida=True
            pass
        
        else:
            print("OPCION INVALIDA")
            pass
        
        pass

main()

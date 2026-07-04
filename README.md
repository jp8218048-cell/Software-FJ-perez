# Software-FJ-perez
Jorge Pérez-programación 
 ofrece varios tipos de servicios (reservas de salas, alquiler de equipos y asesorías especializadas). 
from abc import ABC, abstractmethod

class Entidad(ABC):
    def __init__(self, id):
        self._id = id
    @abstractmethod
    def mostrar_info(self):
        pass
        class ClienteError(Exception):
    pass
class ServicioError(Exception):
    pass
class ReservaError(Exception):
    pass
    import logging
logging.basicConfig(
    filename="logs/eventos.log",
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)
def registrar(mensaje):
    logging.info(mensaje)
def registrar_error(error):
    logging.error(error)
    from entidad import Entidad
from excepciones import ClienteError
class Cliente(Entidad):
    def __init__(self,id,nombre,correo):
        super().__init__(id)
        if nombre == "":
            raise ClienteError("Nombre vacío")
        if "@" not in correo:
            raise ClienteError("Correo inválido")
        self.__nombre=nombre
        self.__correo=correo
    @property
    def nombre(self):
        return self.__nombre
    def mostrar_info(self):
        return f"{self.__nombre} - {self.__correo}" 
    def descripcion(self):
        return "Reserva de Sala"
class ServicioEquipo(Servicio):
    def calcular_costo(self,horas=1,descuento=0):
        return (self.precio*horas)-descuento
    def descripcion(self):
        return "Alquiler de Equipos"
class ServicioAsesoria(Servicio):
    def calcular_costo(self,horas=1,descuento=0):
        return (self.precio*horas)-descuento
    def descripcion(self):
        return "Asesoría Especializada"
        from excepciones import ReservaError
class Reserva:
    def __init__(self,cliente,servicio,horas):
        if horas<=0:
            raise ReservaError("Horas inválidas")
        self.cliente=cliente
        self.servicio=servicio
        self.horas=horas
        self.estado="Pendiente"
    def confirmar(self):
        self.estado="Confirmada"
    def cancelar(self):
        self.estado="Cancelada"
    def procesar(self):
        if self.estado=="Cancelada":
            raise ReservaError("La reserva fue cancelada")
        return self.servicio.calcular_costo(self.horas)
    def __str__(self):
        return f"{self.cliente.nombre} - {self.servicio.descripcion()} - {self.estado}"
        from cliente import Cliente
from servicio import *
from reserva import Reserva
from logger import registrar, registrar_error

clientes=[]
reservas=[]

operaciones=[
    ("cliente",1,"Jorge Pérez","jorge@gmail.com"),
    ("cliente",2,"Ana","ana@gmail.com"),
    ("cliente",3,"","correo"),
    ("cliente",4,"Carlos","carlosgmail.com"),
    ("reserva",),
]

# Clientes válidos

try:
    c1=Cliente(1,"Jorge Pérez","jorge@gmail.com")
    clientes.append(c1)
    registrar("Cliente registrado")

except Exception as e:
    registrar_error(e)

try:
    c2=Cliente(2,"Laura","laura@gmail.com")
    clientes.append(c2)
    registrar("Cliente registrado")

except Exception as e:
    registrar_error(e)

# Cliente inválido

try:
    c3=Cliente(3,"","correo")

except Exception as e:
    registrar_error(e)

# Servicios

sala=ServicioSala("Sala Premium",50000)
equipo=ServicioEquipo("Computador",35000)
asesoria=ServicioAsesoria("IA",80000)

# Reserva válida
try:
    r1=Reserva(c1,sala,3)
    r1.confirmar()
    print(r1)
    print(r1.procesar())
    registrar("Reserva confirmada")
except Exception as e:
    registrar_error(e)
# Reserva inválida
try:
    r2=Reserva(c2,equipo,-5)
except Exception as e:
    registrar_error(e)
# Cancelación
try:
    r3=Reserva(c2,asesoria,2)
    r3.cancelar()
    print(r3.procesar())
except Exception as e:
    registrar_error(e)
# Try Except Else
try:
    total=sala.calcular_costo(5)
except Exception as e:
    registrar_error(e)
else:
    print(total)
# Finally

try:
    x=10/2
except Exception as e:
    registrar_error(e)
finally:
    print("Programa continúa ejecutándose.")
# Encadenamiento
try:
    try:
        int("ABC")
    except ValueError as e:
        raise RuntimeError("Conversión fallida") from e
except Exception as e:
    registrar_error(e)
print("Sistema funcionando correctamente.")
git init
git add .
git commit -m "Sistema Integral de Gestión Software FJ"
git branch -M main
git remote add origin https://github.com/USUARIO/SistemaGestionSoftwareFJ.git
git push -u origin main

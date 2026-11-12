#                        # sistema-de-e-commerce
 

Sistema de gestión escrito en **Go** que permite a los clientes de un gimnasio
**registrarse**, **consultar ropa deportiva, accesorios y suplementos**,
**armar su carrito de compras** y **gestionar su membresía mensual o anual**

## Objetivos

**Objetivo general**

Planificar y estructurar un sistema de gestión de software en Go con enfoque de
programación funcional, organizado en módulos y paquetes con funciones
definidas, como base para su evolución hacia una aplicación web.

**Objetivos específicos del sistema**
1. Delimitar el alcance del sistema, identificando a sus usuarios y las
   funcionalidades que ofrecerá, y organizarlas en módulos con
   responsabilidades definidas.
   
2. Diseñar la estructura del proyecto en Go, con un paquete por módulo y
   dependencias en una sola dirección, declarando funciones con sus
   parámetros y retornos según los principios de la programación funcional.

  **Objetivos específicos de la funcionalidad de la aplicación**

1.	Gestionar un catálogo de ropa deportiva, accesorios, suplementos con precios, manejando un stock .
   
2.	Permitir al cliente armar un carrito, pagar con distintos métodos y dar seguimiento al estado de su pedido.
  
3.	Administrar membresías mensuales y anuales: alta, consulta, renovación y cancelación.



  
  ## Alcance

**El sistema sí puede**

 - Organizar sus funcionalidades en módulos independientes, cada uno programado como un paquete de Go.
 - Gestionar sus operaciones mediante funciones que reciben datos, los validan y devuelven un resultado o un error.
 - Aplicar funciones de orden superior para filtrar información sin modificar el código existente.

**El sistema no puede (en esta etapa)**

- Ofrecer interfaz gráfica o web; se ejecuta desde la terminal.
- Exponer servicios web ni procesar pagos reales.
- Guardar información de forma permanente
- Modelar entidades con `structs`, interfaces o encapsulación formal.
- Atender a varios usuarios a la vez ni controlar acceso por roles.



##  Módulos y paquetes


| Módulo del sistema                 | Paquete Go                           | Responsabilidad |
|------------------------------------|--------------------------------------|-------------------------------------------|
| Usuarios                           |  usuarios                            | Cuentas de clientes: registro, inicio de sesión y datos básicos. |
| Catálogo de ropa y accesorios      |  catalogo                            | Ropa deportiva, calzado y accesorios (guantes, tomatodos, cinturones). |
| Suplementos alimenticios           |  suplementos                         | Proteínas, creatina, pre-entrenos, vitaminas. |
| Carrito de compras                 |  carrito                             | Productos que el cliente va a comprar (ropa, accesorios y suplementos). |
| Suscripciones                      |  suscripciones                       | Membresías del gimnasio. |

### Funciones principales

| Paquete         |     Función        |       Parámetros                      |                   Retorno                             |
|-----------------|--------------------|---------------------------------------|-------------------------------------------------------|
|  usuarios       | RegistrarUsuario   | cedula, nombre, correo, clave string` | error                                                 |
|  usuarios       | IniciarSesion      | correo, clave string`                 | string, error                                         |
|  catalogo       | AgregarProducto    | codigo, nombre, categoria string, precio float64, cantidad int                 | error        |
|  catalogo       | FiltrarProductos   | criterio func(string) bool`           | []string                                              |
|  suplementos    | AgregarSuplemento  | codigo, nombre, tipo, sabor string, precio float64, cantidad int, vence string | error        |
|  suplementos    | ListarPorTipo      | tipo string`                          | []string                                              |
|  carrito        | AgregarAlCarrito   | usuarioID, codigo string, cantidad int| error                                                 |
|  carrito        | CalcularTotal      | usuarioID string`                     | float64, error                                        |
|  suscripciones  | Suscribir          | usuarioID, plan string`               | float64, error                                        |
|  suscripciones  | RenovarSuscripcion | usuarioID string                      | float64, error                                        |

## Paquetes que se incorporan

No se usan paquetes de terceros; solo la biblioteca estándar de Go.

| Paquete     | Uso |
|-------------|-----|
|  fmt        | Mostrar mensajes en consola. |
|  errors     | Devolver errores de validación. |
|  strings    | Validar correos e identificar códigos de suplementos. |
|  sort       | Ordenar los listados. |
|  time       | Fechas de vencimiento de suplementos y membresías. |

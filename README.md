# Vue 3 – CRUD Users

CRUD de usuarios desarrollado con **Vue 3** utilizando **Composition API**.  
La aplicación permite cargar usuarios desde una API pública y gestionar la información de manera local.



## Features

- Carga dinámica de usuarios desde una API
- Listado de usuarios en tabla
- Crear nuevos usuarios (estado local)
- Editar usuarios existentes
- Eliminar usuarios con confirmación
- Formularios en modales
- Validación de email
- Diseño responsive



## Tech Stack

- Vue 3
- Composition API
- Vite
- JavaScript
- HTML5
- CSS3



## Arquitectura y decisiones técnicas

- Uso de **Composition API** para mejor organización y escalabilidad
- Componentes reutilizables (`UsersTable`, `UsersForm`, `Modal`)
- Comunicación entre componentes mediante **props y emits**
- Manejo de estado local con `ref`
- Separación clara de responsabilidades por componente



##  Cómo ejecutar el proyecto
1. Clonar el repositorio:
    ```
    git clone https://github.com/Cali9412/vue-crud-users
    ```

2. Instalar dependencias:
    ```
    npm install    
    ```
3. Ejecutar en modo desarrollo:    
    ```
    npm run dev
    ```

4. Copiar la URL proporcionada en el navegador para visualizar la   aplicación.

##  Notas
Los cambios de usuarios se manejan en estado local, no se persisten en la API.

## Autor
Carlos Zamora\
<sub>Ingeniero Electrónico | Web Developer</sub>

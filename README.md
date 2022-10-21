# Notas del curso de MongoDB

> Domingo 25 de septiembre de 2022.
>
> Requisitos previos: Conceptos básicos de JavaScript
>
> By Gustavo Angel Montoya Martínez



## ¿Qué es?

Es una base de datos de proposito general opensource NoSql que se enfoca en cantidades grandes y rapidas de información.

Esta orientada a documentos(datos) sin esquemas que nos permite ser escalada horizontalmente


## Comandos

Notas:

> Mongo NO tiene estructura de una tabla como base de datos relacionales
>
> NameCollection = Es una variable en este texto, aquí va el nombre de la colección
>
> NameDB = Es una variable en este texto, aquí va el nombre de la Base de datos
>
> Cuando se guarda una colección se genera un id, eso es por parte de mongodb
>
> Mongodb modifica los datos para que el los entienda, por ejemplo el new date
>
> Se pueden guardar listas e incluso objetos dentro del objetos

### Base de datos

Ver base de datos: 
```
show dbs
```

Usar/crear una base de datos: 
```
use NameDB
```

> Sí se crea una base de datos, pero no se genera ninguna colección dentro de ella, no se guarda

Ver la base de datos actual: 
```
db
```

Eliminar base de datos: 
```
db.dropDatabase()
```

> Se elimina la base de datos que se este usando, por eso siempre es recomendable ver cual es la base de datos actual


### Colecciones

Ver las colecciones: 
```
show collections
```

Crear una colección: 
```
db.CreateCollection("NameCollection")
```

> Tambien se pueden crear un colección insertando un documentos en una colección que no existe, MongoDB va a crear la colección por ti

Eliminar colecciones: 
```
db.NameCollection.drop()
```

## Documentos


### Insertar

Crear un documentos: 
```
db.NameCollection.insert({"nombre":"algo"})
```

> Se puede insertar un dato en una colección que no existe, MongoDB va a crear la colección por nosotros.

Ver documentos dentro de las colecciones: 
```
db.NameCollection.find()
```

Ver documentos dentro de las colecciones $bonito$: 
```
db.NameCollection.find().pretty()
```

Guardar varias documentos a la vez:

> Se pueden guardar varios documentos a la vez, en un lugar de pasarle un objeto se puede pasar una lista de objetos.


### Buscar

Buscar documento: 
```
db.NameCollection.find({"algo":"algo"})
```

> Se pueden meter mas filtros por ejemplo: 
> ```
> db.NameCollection.find({"algo":"algo","algo2":"algo2","algo3":"algo3"})
> ```

Buscar documentos **PERO** devuelve solo uno: 
```
db.NameCollection.finOne({"algo":"algo"})
```

> Te devuelve el primero 

Buscar un documento **PERO** muestra datos especificos del objetos: 
```
db.NameCollection.find({"algo":"algo"},{"name":1,"descripcion":1,"_id":0})
```

Ordenar los resultados de la busqueda de documentos: 
```
db.NameCollection.fin({"algo":"algo"}).sort({"name":1})
```

Limitar el numero de resultado: 
```
db.NameCollection.find({"algo":"algo"}).limit(2)
```

Contar cuantos documentos hay en una colección: 
```
db.NameCollection.count()
```

> El comando sirve, pero es mas actaul `db.NameCollection.countDocuments()`

Funciones en documentos: 
```
db.NameCollection.find().forEach(productos=>print("Productos: "+ productos.nombre))
```

### Actualizar

Actualizar un objetos: 
```
db.NameCollection.update({"algo":"algo"},{$set:{"algo"}:{"algo"}})
```
> La función update recibe dos objetos, el primero es el filtro de busqueda y el seguno es la nueva información.

Insertar un objeto si no hay coincidencias: 
```
db.NameCollection.update({"algo":"algo"},{$set:{"algo":"algo"}},upsert:ture)
```

Incrementar datos numeros : 
```
db.NameDocument.update({"algo":"algo"},{$inc:{"algo":0.1}})
```

Renombrar un valor del documento: 
```
db.NameCollection.update({"algo":"algo"},{$rename:{"algo":"algo"}}) 
```
> A diferencia del $set, el $rename cambiar el titulo de la propiedad no el atributo

### ELiminar

Eliminar un documento: 
```
db.NameCollection.remove({"algo":"algo"})
```

> Los parametros que recibe son para la busqueda del elemento a eliminar y aunque funciona el comando es mas nuevo el removeOne, removeMany.

Para eliminar todos los documentos a la vez: 
```
db.NameCollection.remove({})
```

Para crear un backup de nuestra base de datos es:

```
mongodump
```

Para restaurar: 
```
mongorestore
```

### Ejemplo para insertar varios:

```
db.productos.insert([
    {
        "nombre":"mouse",
        "descripcions":"gamer",
        "tags":["gamer","computers"],
        "cantidad":12,
        "fechaCreacion": new Date()        
    },
    {
        "nombre":"monitor",
        "descripcions":"lg monitos",
        "tags":["gamer","computers"],
        "cantidad":1,
        "fechaCreacion": new Date()        
    },
    {
        "nombre":"teclado",
        "descripcions":"gamer",
        "tags":["gamer","computers"],
        "cantidad":2,
        "fechaCreacion": new Date()        
    }
    
])
```
